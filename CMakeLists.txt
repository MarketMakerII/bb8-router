cmake_minimum_required(VERSION 3.20)

project(bb8router)

set(CMAKE_C_COMPILER /opt/rh/devtoolset-11/root/usr/bin/gcc)
set(CMAKE_CXX_COMPILER /opt/rh/devtoolset-11/root/usr/bin/g++)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

set(INC_DIR ${PROJECT_SOURCE_DIR}/includes)

if (CMAKE_HOST_WIN32)
    set(WINDOWS 1)
    set(LINK_DIR ${PROJECT_SOURCE_DIR}/lib/win)
elseif (CMAKE_HOST_UNIX)
    set(LINUX 1)
    set(LINK_DIR ${PROJECT_SOURCE_DIR}/lib/linux)
endif()

file(GLOB SOURCES_AND_HEADERS "*.cpp" "includes/**/*.h" "")

include_directories(${INC_DIR} /usr/local/include)
link_directories(${LINK_DIR} /usr/local/lib)

add_executable(bb8router bb8router.cpp bb8router.h)

target_link_libraries(bb8server PUBLIC zmq)