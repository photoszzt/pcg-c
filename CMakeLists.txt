project(pcg-c)
cmake_minimum_required(VERSION 3.21)

set(CMAKE_C_STANDARD 23)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_BUILD_TYPE Release CACHE STRING "Build configuration (Release/Debug)")
set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release")
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

message(STATUS "Build configuration: ${CMAKE_BUILD_TYPE}")
message(STATUS "Install directory: ${CMAKE_INSTALL_PREFIX}")

set(LIBRARY_OUTPUT_PATH    ${CMAKE_BINARY_DIR}/bin)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

add_compile_options("$<$<COMPILE_LANGUAGE:C>:-g;-Wall>")
set(CMAKE_C_EXTENSIONS ON) #...with compiler extensions like gnu++11
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(pcg_c_src 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-advance-128.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-advance-16.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-advance-32.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-advance-64.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-advance-8.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-global-32.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-global-64.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-output-128.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-output-16.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-output-32.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-output-64.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-output-8.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-rngs-128.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-rngs-16.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-rngs-32.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-rngs-64.c
    ${CMAKE_CURRENT_SOURCE_DIR}/src/pcg-rngs-8.c
)
add_library(pcg-c STATIC ${pcg_c_src})
target_include_directories(pcg-c PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
