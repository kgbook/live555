[![Build Status](https://travis-ci.org/kgbook/live555.svg?branch=master)](https://travis-ci.org/kgbook/live555)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](https://github.com/kgbook/RTSPServer)

# live555
A mirror of the live555 source code.
For documentation and instructions for building this software,
see <http://www.live555.com/liveMedia/>

# Build
```shell
chmod +x build.sh
bash build.sh
```

## Install
```cmake
make install -DCMAKE_PREFIX_PATH=/usr/local  
# install on ${CMAKE_SOURCE_DIR}/out by default if CMAKE_PREFIX_PATH macro not defined
```

Uncomment `testProgs` Line in [CMakeLists.txt](CMakeLists.txt) to install the *testProgs*.