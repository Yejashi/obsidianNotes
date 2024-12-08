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
opt -load-pass-plugin ./lib/libHelloWorldPass.so -passes=hello-world -disable-output test_1.ll
```

