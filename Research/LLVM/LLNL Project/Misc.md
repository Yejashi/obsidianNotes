##### Building a pass as a shared library.

Create a directory for build output.
```bash
mkdir build
cd build
```

Run CMake to generate the build system:
```bash
cmake -G "ninja"
```

Compile the pass:
```bash
ninja
```

Template `CMakeLists.txt`:
```
cmake_minimum_required(VERSION 3.22)

project(PassTracker LANGUAGES CXX)

# Locate LLVM
find_package(LLVM REQUIRED CONFIG)

# Include LLVM's CMake modules
list(APPEND CMAKE_MODULE_PATH "${LLVM_CMAKE_DIR}")
include(AddLLVM)

# Add your pass as a shared library
add_llvm_library(PassTracker MODULE
    src/custom_pass.cpp
)

# Ensure proper include paths and C++ version
target_include_directories(PassTracker PRIVATE ${LLVM_INCLUDE_DIRS})
target_compile_features(PassTracker PRIVATE cxx_std_17)

# Define required macros and link dependencies
target_compile_definitions(PassTracker PRIVATE ${LLVM_DEFINITIONS})
target_link_libraries(PassTracker PRIVATE LLVMCore LLVMSupport)
```

##### Running the pass with Clang

Compile the target code to LLVM IR