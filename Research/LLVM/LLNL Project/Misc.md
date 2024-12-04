Building a pass as a shared library.

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
