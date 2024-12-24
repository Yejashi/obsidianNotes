##### Building a pass as a shared library.

Create a directory for build output.
```bash
mkdir build
cd build
```

Run CMake to generate the build system:
```bash
cmake -G "Ninja" ..
```

Compile the pass:
```bash
ninja
```

Template `CMakeLists.txt`:
```
cmake_minimum_required(VERSION 3.22)

project(HelloWorldPass LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

#set(PASS_MANAGER_TYPE "legacy_manager")
set(PASS_MANAGER_TYPE "new_manager")

# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-mangle")


# Ensure libraries are placed in the lib directory
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib)

# Locate LLVM
find_package(LLVM 14.0.6 REQUIRED CONFIG)

# Include LLVM's CMake modules
list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")

include(AddLLVM)

add_library(HelloWorldPass SHARED src/${PASS_MANAGER_TYPE}/hello_world_pass.cpp)

# Include necessary directories
target_include_directories(HelloWorldPass PRIVATE 
    ${LLVM_INCLUDE_DIRS} 
    ${CMAKE_SOURCE_DIR}/include/${PASS_MANAGER_TYPE}
)

# target_link_libraries(HelloWorldPass PRIVATE LLVMCore)
target_link_libraries(HelloWorldPass PRIVATE LLVMDemangle)

```

##### Running the pass with Clang

Compile the target code to LLVM IR
```
clang++ -O0 -Xclang -disable-O0-optnone -emit-llvm -S -o test_1.ll ../sample_programs/test_1.cpp 
```
- `-XClang`: This flag allows you to pass arguments directly to the Clang compiler backend (instead of the frontend). It's used to give Clang-specific options that wouldn't normally be passed through the standard command-line flags.
- `-disable-O0-optnone`: This option disables the `-optnone` attribute at optimization level `O0`. Normally, Clang inserts this attribute when `-O0` is specified, which disables certain optimizations even if they're explicitly requested. This flag ensures that no such attribute is added, allowing you to keep some optimizations even at `O0`.

Apply the pass to the LLVM IR
```
opt -O1 -load-pass-plugin ./lib/libhello_world_pass_instrumentation.so  -disable-output test_1.ll
```



### Simple Pass Instrumentation approach

#### LLVM
1. Get the name of every pass.
2. Get the line number of every pass.
3. Get the function the pass is called in.
4. Get whether the pass succeded.


### Dec 17 Meeting
#### Read Dyninst paper: [Link](https://dl.acm.org/doi/pdf/10.1145/2024569.2024572)



### **Code Injection Based on Caliper Regions**

1. **Objective**: Easier to perform code injection at compile time and runtime.
2. **Steps**:
    - **Compile Time**:
        - Build a collection of attributes.
        - Inject code into the program using a Clang pass.
    - **Runtime**:
        - As the program runs, the compiler receives remark information and injects relevant attributes into the source code dynamically.
3. **Clang Pass**:
    - Reads remark information.
    - Injects `cali_set_attribute` calls into the source code with the relevant information.

---

### **Static Pass and Runtime Stitching**

- **Compile Time**:
    - Gather all relevant information using Caliper.
    - Output this information in a structured format.
- **Runtime**:
    - A Caliper service checks annotations during program execution.
    - Stitch together runtime attributes using the compile-time output.
    - Update attributes in Caliper as needed.

---

### **Call Tree Challenges**

- At compile time, there is no reliable way to determine the call tree.
- **Solution**:
    - Collect relevant remark information at compile time.
    - Merge and refine this information at runtime.

---

### **Understanding HPCStruct in HPCToolkit**

1. **Function**:
    - Maps measured performance data to the corresponding source code locations.
2. **Components**:
    - **Dineinst**: Instrumentation and analysis tool.
3. **Next Steps**:
    - Read relevant papers on HPCStruct and Dineinst.
    - Reuse Dineinst functionalities where applicable.

---