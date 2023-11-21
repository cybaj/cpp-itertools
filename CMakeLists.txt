cmake_minimum_required(VERSION 3.10)

project(MyDynamicLib VERSION 1.0)

# Ensure correct default build type (Debug/Release/...)
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Default build type" FORCE)
endif()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Use C++11 standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Define the library
add_library(MyDynamicLib SHARED
    src/hello.cpp
)

target_include_directories(MyDynamicLib PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# Optional: if you want to build tests
enable_testing()
add_executable(TestMyDynamicLib tests/test_main.cpp)
target_link_libraries(TestMyDynamicLib MyDynamicLib)
add_test(NAME TestMyDynamicLib COMMAND TestMyDynamicLib)

