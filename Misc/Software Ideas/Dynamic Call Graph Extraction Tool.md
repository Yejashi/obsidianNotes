## Motivation

Current dynamic/statica call graph tools are either very expensive or inaccurate. A hubrid approach is needed.


# Complete Breakdown of Each Step

## Step 1: Early Pass for Static Analysis

**Purpose:** Build the baseline call graph from source code before compiler optimizations obscure the structure.
**What it does:**

```cpp
// Input: Your source code in LLVM IR (early pipeline)
void processData() {
    validate();      // Direct call - statically known
    transform();     // Direct call - statically known
    callback_ptr();  // Indirect call - unknown target
}
```

**Output: static_callgraph.json**

```json
{
  "functions": [
    {
      "symbol": "processData()",
      "mangled": "_Z11processDatav",
      "source_file": "main.cpp",
      "line": 42,
      "direct_calls": [
        {
          "target": "validate()",
          "target_mangled": "_Z8validatev",
          "line": 43,
          "basic_block_id": "bb_2"
        },
        {
          "target": "transform()",
          "target_mangled": "_Z9transformv",
          "line": 44,
          "basic_block_id": "bb_3"
        }
      ],
      "indirect_calls": [
        {
          "call_site_id": "cs_042_001",
          "line": 45,
          "basic_block_id": "bb_4",
          "call_type": "function_pointer"
        }
      ]
    }
  ]
}
```

**Why early pipeline?**

- Before inlining: You see `A() -> B()` even if B gets inlined later
- Before devirtualization: Virtual calls remain virtual (not optimized away)
- Before dead code elimination: See all possible paths
- Matches source code structure that developers understand

**What you capture:**
- ✅ All direct call edges (the "easy" part of the graph)
- ✅ Location of indirect calls (but not their targets yet)
- ✅ Source line/file information for visualization
- ✅ Basic block IDs for coverage correlation

---

## Step 2: Instrument Indirect Calls in YOUR Code
**Purpose:** Discover the runtime targets of calls that can't be resolved statically (virtual functions, function pointers, lambdas).

**What to instrument:**

```cpp
// Virtual function call
class Base {
    virtual void process() = 0;
};

Base* obj = getDerivedObject();
obj->process();  // <-- We don't know which process() at compile time
```

**Instrumentation inserted:**

```cpp
// Before optimization, the indirect call site looks like:
void* vtable_entry = obj->vtable[process_index];

// Your instrumentation adds:
__trace_indirect_call("cs_042_001", vtable_entry);

// Then the actual call:
((void(*)(Base*))vtable_entry)(obj);
```

**Runtime behavior:**

```cpp
void __trace_indirect_call(const char* call_site_id, void* target_addr) {
    // Thread-local lock-free buffer
    CallRecord record = {
        .call_site_id = call_site_id,
        .target_addr = (uintptr_t)target_addr,
        .timestamp = get_timestamp()  // optional
    };
    
    thread_local_buffer.append(record);
    
    // Periodic flush to file when buffer fills
    if (thread_local_buffer.is_full()) {
        flush_to_file();
    }
}
```

**Output: indirect_calls.log** (binary format for efficiency)

```
cs_042_001,0x55a3c8001234
cs_042_001,0x55a3c8001450  // Same call site, different target (polymorphism)
cs_103_005,0x55a3c8002100
...
```

**Why only indirect calls?**

- Direct calls are already in static graph (free!)
- Instrumentation overhead is proportional to # of call sites instrumented
- Indirect calls are typically <5-10% of all calls in most code
- This is the **surgical precision** that makes your approach fast

**What you capture:**

- ✅ Which virtual function implementation was actually called
- ✅ Which function a function pointer pointed to at runtime
- ✅ Lambda targets
- ✅ Can see if same call site dispatches to multiple targets

---

## Step 3: Instrument Function Entries (Catch Callback Invocations)

**Purpose:** Discover when YOUR functions are called FROM library code that you don't instrument.

**The problem this solves:**
```cpp
// Your code - you instrument this
void myComparator(int a, int b) {
    return a < b;
}

void foo() {
    std::sort(vec.begin(), vec.end(), myComparator);
}

// Library code (libstdc++) - you DON'T instrument this
namespace std {
    template<typename Compare>
    void sort(..., Compare comp) {
        // ... sorting logic ...
        comp(arr[i], arr[j]);  // <-- This call site is NOT instrumented!
    }
}
```

**Without function entry instrumentation:**

- You see: `foo() -> std::sort()`
- You DON'T see: `std::sort() -> myComparator()`
- **Missing edge!**

**Instrumentation added:**

```cpp
void myComparator(int a, int b) {
    // Inserted at function entry by your pass
    __trace_function_entry(
        "myComparator",                      // Function name
        __builtin_return_address(0)          // Who called me?
    );
    
    // Original function body
    return a < b;
}
```

**Runtime behavior:**
```cpp
void __trace_function_entry(const char* func_name, void* return_addr) {
    // Record who called this function
    EntryRecord record = {
        .function = func_name,
        .caller_addr = (uintptr_t)return_addr
    };
    
    entry_buffer.append(record);
}
```

**Output: function_entries.log**

```
myComparator,0x7f8a3c123456    // return address in libstdc++.so
myThreadFunc,0x7f8a3d234567    // return address in libpthread.so
signalHandler,0x7f8a3e345678   // return address in libc.so (signal trampoline)
```

**Postprocessing resolution:**

```python
# Later, resolve addresses to symbols
caller_info = resolve_address(0x7f8a3c123456)
# Returns: {
#   "library": "libstdc++.so.6",
#   "symbol": "std::sort<...>::operator()",  # if available
#   "offset": "+0x234"
# }

# Now you know: std::sort called myComparator
graph.add_edge("std::sort", "myComparator", 
               type="callback", 
               through_library=True)
```

**Why this works:**

- `__builtin_return_address(0)` gives the address of the instruction after the `call`
- You can resolve this to see which library/function called you
- Catches ALL cases where library code calls your code

**Overhead consideration:**

- Every function entry has overhead (not just indirect calls)
- But still cheaper than full call tracing
- Can optimize: only instrument functions whose address is taken
    - Your pass can detect: `&myFunction` or function used as template arg
    - Only those functions need entry instrumentation

---

## Step 4: Pattern Matching for Common Library APIs

**Purpose:** Statically identify where you're passing callbacks to known library functions, creating candidate edges even before runtime.

**What it does:**
```cpp
// Your pass analyzes call sites
void foo() {
    std::thread t(myThreadFunction);           // Pattern 1
    pthread_create(&tid, NULL, myFunc, NULL);  // Pattern 2
    std::sort(vec.begin(), vec.end(), myCmp);  // Pattern 3
    signal(SIGINT, myHandler);                 // Pattern 4
}
```

**Your pass recognizes these patterns:**

```python
# In your LLVM pass
if (CallInst->getCalledFunction()->getName() == "pthread_create") {
    Value* callback_arg = CallInst->getArgOperand(2);
    if (Function* callback = dyn_cast<Function>(callback_arg)) {
        // Found: pthread_create called with myFunc
        json_output["callback_registrations"].append({
            "api": "pthread_create",
            "caller": current_function,
            "callback": callback->getName(),
            "line": get_line_number(CallInst),
            "confidence": "static"
        });
    }
}
```

**Pattern database (built into your pass):**
```cpp
struct LibraryAPIPattern {
    std::string function_name;
    int callback_arg_index;
    std::string library;
} known_patterns[] = {
    {"pthread_create", 2, "libpthread"},
    {"signal", 1, "libc"},
    {"std::thread::thread", 0, "libstdc++"},
    {"std::for_each", 2, "libstdc++"},
    {"qsort", 3, "libc"},
    {"atexit", 0, "libc"},
    // ... hundreds more
};
```

**Output: callback_registrations.json**
```json
{
  "registrations": [
    {
      "caller": "foo",
      "api": "pthread_create",
      "library": "libpthread",
      "callback": "myThreadFunction",
      "line": 67,
      "confidence": "static",
      "call_site_id": "reg_067_001"
    },
    {
      "caller": "processData",
      "api": "std::sort",
      "library": "libstdc++",
      "callback": "myComparator",
      "line": 103,
      "confidence": "static",
      "call_site_id": "reg_103_001"
    }
  ]
}
```

**Why this is useful:**
1. **Creates candidate edges before runtime**
    - You know `foo` likely causes `pthread_create -> myThreadFunction`
    - Even if the program hasn't run yet
2. **Validates against runtime data**
    - If `myThreadFunction` executes AND you see it was entered from libpthread
    - Confirms the edge with high confidence
3. **Handles cases where entry instrumentation is ambiguous**
    - Entry instrumentation: "myComparator was called from libstdc++"
    - Pattern matching: "std::sort was called with myComparator"
    - Together: "std::sort called myComparator" (definitive)
4. **Documentation/visualization**
    - Can label edges: "via pthread_create" instead of generic "via libpthread"
    - Better UX for developers

**Limitations:**
- Only works for APIs you've added to the pattern database
- Custom library callbacks won't be recognized (falls back to entry instrumentation)
- Template instantiations can be tricky (need name mangling awareness)

---

## Step 5: Coverage-Based Pruning
**Purpose:** Remove edges from the static graph that weren't actually executed, giving you the _dynamic_ call graph.
**The problem:**

```cpp
void foo(bool flag) {
    if (flag) {
        pathA();  // Line 10
    } else {
        pathB();  // Line 12
    }
    pathC();      // Line 14
}

// Your test run: foo(true) is called
```

**Static graph shows:**

```
foo -> pathA
foo -> pathB  
foo -> pathC
```

**But at runtime, only:**

```
foo -> pathA
foo -> pathC
```

**Coverage tells you which lines executed:**

Using llvm-cov with basic block coverage:

```bash
llvm-cov show --format=json app -instr-profile=app.profdata > coverage.json
```

**coverage.json excerpt:**

```json
{
  "functions": [
    {
      "name": "foo",
      "regions": [
        {"line": 10, "col": 5, "count": 1},   // pathA() call
        {"line": 12, "col": 5, "count": 0},   // pathB() call - NOT EXECUTED
        {"line": 14, "col": 5, "count": 1}    // pathC() call
      ]
    }
  ]
}
```

**Pruning algorithm:**

```python
def prune_static_graph(static_graph, coverage_data):
    dynamic_graph = copy(static_graph)
    
    for function in dynamic_graph.functions:
        for call_site in function.call_sites:
            # Get coverage for this call site's basic block
            bb_id = call_site.basic_block_id
            exec_count = coverage_data.get_execution_count(bb_id)
            
            if exec_count == 0:
                # This call site never executed
                call_site.mark_not_executed()
                # Don't remove target function yet! It might be called elsewhere
            else:
                # This call site executed
                call_site.execution_count = exec_count
    
    # Now remove unreachable functions
    reachable = compute_reachability(dynamic_graph, entry_points)
    dynamic_graph.functions = [f for f in dynamic_graph.functions 
                                if f in reachable]
    
    return dynamic_graph
```

**Important subtlety:**

```cpp
void foo() { bar(); }  // Line 5
void baz() { bar(); }  // Line 8

// Run: Only foo() is called
```

**Naive pruning:**

- Line 5 executed → keep `foo -> bar`
- Line 8 not executed → remove `baz -> bar`
- Remove bar()? NO! It's reachable via foo()

**Correct pruning:**

1. Mark which **edges** were taken (call sites executed)
2. Compute **reachability** from entry points via executed edges
3. Keep all reachable functions
4. Remove unreachable functions and dead edges

**What you get:**

- ✅ Only code paths that actually executed
- ✅ Dead code identified (in static graph but not dynamic)
- ✅ Test coverage visualization (which edges tested)
- ✅ Can compare multiple runs (different inputs → different paths)

---

## Step 6: Postprocessing to Connect Callback Chains

**Purpose:** Combine all the data sources to build the complete dynamic call graph with library-mediated callbacks.

**Inputs:**

1. `static_callgraph.json` - Direct call edges
2. `indirect_calls.log` - Runtime indirect call targets
3. `function_entries.log` - Who called your functions
4. `callback_registrations.json` - Statically identified callbacks
5. `coverage.json` - What actually executed

**Algorithm:**

```python
def build_dynamic_callgraph(static_graph, indirect_calls, 
                           function_entries, callback_regs, coverage):
    # Start with static graph
    graph = load_graph(static_graph)
    
    # === STEP 6A: Resolve indirect calls ===
    for call_site_id, target_addr in indirect_calls:
        # Find the call site in static graph
        call_site = graph.find_call_site(call_site_id)
        
        # Resolve address to symbol
        target_symbol = resolve_address_to_symbol(target_addr)
        
        # Replace indirect edge with concrete edge
        call_site.add_concrete_target(target_symbol)
    
    # === STEP 6B: Connect library callbacks ===
    # Build a map: which functions were entered from library code?
    library_calls = {}
    for func_name, return_addr in function_entries:
        caller_info = resolve_address(return_addr)
        if caller_info.is_library():
            library_calls[func_name] = caller_info
    
    # Match with callback registrations
    for registration in callback_regs:
        callback = registration.callback
        api = registration.api
        caller = registration.caller
        
        # Did this callback actually execute?
        if callback in library_calls:
            # Yes! And we know which library called it
            library_info = library_calls[callback]
            
            # Create edge chain: caller -> api -> callback
            graph.add_edge(caller, api, type="library_call")
            graph.add_edge(api, callback, 
                          type="callback",
                          library=library_info.library,
                          confidence="confirmed")
        else:
            # Callback registered but never executed
            # Add as "potential" edge if you want, or skip
            pass
    
    # Handle entry instrumentation for unknown APIs
    for func_name, return_addr in function_entries:
        caller_info = resolve_address(return_addr)
        if caller_info.is_library() and func_name not in callback_regs:
            # Unknown library called this function
            # We don't know which of your functions caused it
            # Add edge from library to function
            graph.add_edge(f"<{caller_info.library}>", func_name,
                          type="callback_unknown_source",
                          confidence="detected")
    
    # === STEP 6C: Prune based on coverage ===
    for edge in graph.edges:
        if edge.call_site_id:
            bb_id = edge.basic_block_id
            if coverage.get_count(bb_id) == 0:
                edge.mark_not_executed()
    
    # Remove unreachable nodes
    graph = compute_reachable_subgraph(graph)
    
    # === STEP 6D: Build transitive callback chains ===
    # If: foo -> pthread_create -> threadFunc -> processData
    # Mark processData as "transitively called by foo via thread"
    graph.compute_transitive_closure(mark_library_hops=True)
    
    return graph
```

**Example output: dynamic_callgraph.json**

```json
{
  "functions": [...],
  "edges": [
    {
      "source": "main",
      "target": "processData",
      "type": "direct",
      "executed": true,
      "execution_count": 1
    },
    {
      "source": "processData",
      "target": "std::sort",
      "type": "direct",
      "executed": true,
      "execution_count": 3
    },
    {
      "source": "std::sort",
      "target": "myComparator",
      "type": "callback",
      "through_library": "libstdc++.so.6",
      "registered_at": "processData:103",
      "confidence": "confirmed",
      "executed": true,
      "execution_count": 156  // Called many times during sort
    },
    {
      "source": "main",
      "target": "pthread_create",
      "type": "direct",
      "executed": true
    },
    {
      "source": "pthread_create",
      "target": "workerThread",
      "type": "callback",
      "through_library": "libpthread.so.0",
      "registered_at": "main:45",
      "confidence": "confirmed",
      "executed": true
    }
  ]
}
```

**Why this step is crucial:**

1. **Synthesizes all data sources**
    - No single instrumentation captures everything
    - Combining them gives complete picture
2. **Resolves ambiguities**
    - Entry instrumentation: "called from libstdc++"
    - Pattern matching: "std::sort was passed myComparator"
    - Together: "std::sort called myComparator" ✓
3. **Validates static analysis**
    - Static: "this MIGHT be called as callback"
    - Dynamic: "this WAS called as callback"
    - Confidence levels for edges
4. **Handles complex chains**
    
    ```
    main 
      -> pthread_create 
        -> workerThread 
          -> std::sort 
            -> myComparator
    ```
    
    Without postprocessing, you'd have disconnected pieces

---

## Summary: Why All 6 Steps Are Needed

|Step|What It Captures|What It Misses|Overhead|
|---|---|---|---|
|1. Static analysis|Direct calls, call sites|Runtime targets, execution|Compile-time only|
|2. Indirect call instrumentation|Virtual/pointer targets|Library→code calls|Low (~0.5-2x)|
|3. Function entry instrumentation|Library→code calls|Which registration caused it|Medium (~1-3x)|
|4. Pattern matching|API semantics, callback intent|Unknown APIs|Compile-time only|
|5. Coverage pruning|What actually executed|-|Low (~1.5-2x)|
|6. Postprocessing|Complete picture|-|Offline|

**Total runtime overhead: ~2-5x** (much better than 10-100x full tracing)

**Completeness: ~95-99%** (missing only exotic cases like dlsym'd callbacks)

Each step fills a gap left by the others, creating a complete source-level dynamic call graph.