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
clang -O0 -Xclang -disable-O0-optnone -emit-llvm -S -o target.ll target.c
```
- `-XClang`: 

Apply the pass to the LLVM IR
```
opt -load-pass-plugin ./PassTracker.so -passes="pass-tracker" -disable-output target.ll
```

