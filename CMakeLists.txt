cmake_minimum_required(VERSION 3.22)
project(julia_synth C CXX)
set(CMAKE_C_STANDARD 23)

find_library(libsoundio NAMES soundio)
add_library(julia_synth SHARED playback.hpp)
target_include_directories(julia_synth PUBLIC "${CMAKE_SOURCE_DIR}/..")

set_target_properties(julia_synth PROPERTIES
    LINKER_LANGUAGE CXX
)
target_link_libraries(julia_synth PUBLIC soundio)

add_executable(test main.cpp)
target_link_libraries(test julia_synth)
