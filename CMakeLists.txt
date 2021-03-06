cmake_minimum_required(VERSION 3.2.2)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    # if picobench is built as root, activate folders
    set_property(GLOBAL PROPERTY USE_FOLDERS ON)
endif()

project(picobench)

option(PICOBENCH_BUILD_TOOLS "picobench: build tools" OFF)
option(PICOBENCH_BUILD_TESTS "picobench: build tests" OFF)
option(PICOBENCH_BUILD_EXAMPLES "picobench: build examples" OFF)
option(PICOBENCH_BIND_TO_ONE_CORE "picobench: bind runner to one core (better precision for long benchmarks)" ON)
mark_as_advanced(PICOBENCH_BUILD_TOOLS PICOBENCH_BUILD_TESTS PICOBENCH_BUILD_EXAMPLES PICOBENCH_DONT_BIND_TO_ONE_CORE)

add_library(picobench INTERFACE)
target_sources(picobench INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/include/picobench/picobench.hpp)
target_include_directories(picobench INTERFACE include)
target_compile_features(picobench INTERFACE
    cxx_auto_type
    cxx_delegating_constructors
    cxx_lambdas
    cxx_override
    cxx_range_for
    cxx_right_angle_brackets
)

if(PICOBENCH_BUILD_TOOLS)
    add_subdirectory(tools)
endif()

if(PICOBENCH_BUILD_TESTS)
    add_subdirectory(test)
endif()

if(PICOBENCH_BUILD_EXAMPLES)
    add_subdirectory(example)
endif()
