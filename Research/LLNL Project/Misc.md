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

# Locate LLVM
find_package(LLVM REQUIRED CONFIG)

# Include LLVM's CMake modules
list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")
include(AddLLVM)

# Add your pass as a shared library
add_llvm_library(HelloWorldPass MODULE
    src/hello_world_pass.cpp
)

# Ensure libraries are placed in the lib directory
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib)

# Set the output directory for the shared library
set_target_properties(HelloWorldPass PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH}
)

# Include necessary directories
target_include_directories(HelloWorldPass PRIVATE 
    ${LLVM_INCLUDE_DIRS} 
    ${CMAKE_SOURCE_DIR}/include
)

# Ensure proper include paths and C++ version
target_compile_features(HelloWorldPass PRIVATE cxx_std_17)

# Define required macros and link dependencies
target_compile_definitions(HelloWorldPass PRIVATE ${LLVM_DEFINITIONS})
target_link_libraries(HelloWorldPass PRIVATE LLVMCore LLVMSupport)

```

##### Running the pass with Clang

Compile the target code to LLVM IR
```
clang++ -O0 -Xclang -disable-O0-optnone -emit-llvm -S -o target.ll target.c
```
- `-XClang`: This flag allows you to pass arguments directly to the Clang compiler backend (instead of the frontend). It's used to give Clang-specific options that wouldn't normally be passed through the standard command-line flags.
- `-disable-O0-optnone`: This option disables the `-optnone` attribute at optimization level `O0`. Normally, Clang inserts this attribute when `-O0` is specified, which disables certain optimizations even if they're explicitly requested. This flag ensures that no such attribute is added, allowing you to keep some optimizations even at `O0`.

Apply the pass to the LLVM IR
```
opt -load-pass-plugin ./lib/HelloWorld.so -passes="hello-world" -disable-output test_1.ll
```

