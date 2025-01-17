# 3.8 version is required for `cxx_std_17`
cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

if(NOT DEFINED PROJECT_NAME)
    set(BUILD_AS_STANDALONE ON)
else()
    set(BUILD_AS_STANDALONE OFF)
endif()

project(enum.hpp)

add_library(${PROJECT_NAME} INTERFACE)
target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_17)
target_include_directories(${PROJECT_NAME} INTERFACE headers)

target_compile_options(${PROJECT_NAME}
    INTERFACE
    $<$<OR:$<CXX_COMPILER_ID:Clang>,$<CXX_COMPILER_ID:AppleClang>>:
        -Wno-c++98-compat-pedantic
        -Wno-covered-switch-default
        -Wno-ctad-maybe-unsupported
        -Wno-old-style-cast
        -Wno-shadow
        -Wno-unknown-warning-option
        -Wno-unused-macros
        -Wno-weak-vtables
        >)

if(BUILD_AS_STANDALONE)
    enable_testing()
    add_subdirectory(untests)
endif()
