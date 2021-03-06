cmake_minimum_required (VERSION 3.7)

project (live555)
option(dbg "release or debug" ON)
option(linux-cross "run on target platform" OFF) #linux-cross

set (LIVE555_VERSION_MAJOR "2019")
set (LIVE555_VERSION_MINOR "03")
set (LIVE555_VERSION_PATCH "06")
set (LIVE555_VERSION "${LIVE555_VERSION_MAJOR}.${LIVE555_VERSION_MINOR}.${LIVE555_VERSION_PATCH}")

set(CMAKE_CXX_STANDARD 11)
#set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
#set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/lib)
#set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
set(CMAKE_PREFIX_PATH ${CMAKE_SOURCE_DIR}/out)

if (dbg)
    set(CMAKE_VERBOSE_MAKEFILE ON)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g -O0 -DDEBUG")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2")
    add_definitions(-DNDEBUG)
endif ()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

if (linux-cross)
    add_definitions(-DBSD=1 -DSOCKLEN_T=socklen_t -DNO_STRSTREAM=1 -D_LARGEFILE_SOURCE=1)
elseif (${CMAKE_HOST_SYSTEM_NAME} MATCHES Darwin)
    add_definitions(-DBSD=1 -DSOCKLEN_T=socklen_t -DHAVE_SOCKADDR_LEN=1 -DTIME_BASE=int -DNEED_XLOCALE_H=1)
elseif(${CMAKE_HOST_SYSTEM_NAME} MATCHES Linux)
    add_definitions(-DBSD=1 -DSOCKLEN_T=socklen_t -D_LARGEFILE_SOURCE=1 -D_FILE_OFFSET_BITS=64)
else()
    message(FATAL_ERROR "use Linux or macOS, please!")
endif ()

if (CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive")
endif ()

set(live555_project
        groupsock
        liveMedia
        BasicUsageEnvironment
        UsageEnvironment
#        mediaServer
#        testProgs      # uncoment this line if needed
#        proxyServer
        )

foreach (subproject ${live555_project})
    message(STATUS ${subproject})
    add_subdirectory(${subproject})
endforeach ()
