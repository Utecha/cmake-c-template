cmake_minimum_required(VERSION 3.20)

#-------------------------------------------------------------------------------

set(EXAMPLE example)
set(VERSION 0.0.1)

project(
    ${EXAMPLE}
    VERSION ${VERSION}
    DESCRIPTION "An Example C Project Template"
    LANGUAGES C
)

message("--- ${EXAMPLE} Version ${VERSION} ---")

#-------------------------------------------------------------------------------

# Add the local 'cmake' directory to the CMake module path.
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# Exports compile commands for your LSP.
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Sets the default build type to 'Debug' in the event it's not set.
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug" CACHE STRING "Build Type" FORCE)
    message(STATUS "No build type set. Defaulting to '${CMAKE_BUILD_TYPE}'.")
endif()

# Normalize the binary output directory between platforms and toolchains.
if(WIN32 AND ("${CMAKE_C_COMPILER_ID}" STREQUAL "MSVC"))
    set(OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}")
else()
    set(OUTPUT_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_BUILD_TYPE}")
endif()

#-------------------------------------------------------------------------------

# Load the src directory `CMakeLists.txt`.
add_subdirectory(src)
