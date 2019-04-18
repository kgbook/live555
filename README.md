# live555
A mirror of the live555 source code.
For documentation and instructions for building this software,
see <http://www.live555.com/liveMedia/>

# Build
Build project using cmake.

If you do not want shared library, you should modify value of `shared` from `OFF` to `ON`.

```cmake
mkdir build && cmake .. && make -j2 # static library by default
```

## Install
```cmake
make install -DCMAKE_PREFIX_PATH=/usr/local  
# install on ${CMAKE_SOURCE_DIR}/out by default if CMAKE_PREFIX_PATH macro not defined
```

Uncomment `testProgs` Line in [CMakeLists.txt](CMakeLists.txt) to install the *testProgs*.