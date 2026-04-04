#
# CMake Project Setup
#
cmake_minimum_required(VERSION 3.24)

project(Quake2)

set(CMAKE_C_STANDARD 99)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/out/${CMAKE_C_COMPILER_ID}-${CMAKE_C_COMPILER_ARCHITECTURE_ID}-${CMAKE_BUILD_TYPE}/")
set(CMAKE_PDB_OUTPUT_DIRECTORY ${CMAKE_RUNTIME_OUTPUT_DIRECTORY})

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_ARCHIVE_OUTPUT_DIRECTORY})

#
# Global definitions
#
list(APPEND QUAKE_GDEFS
    _CRT_SECURE_NO_WARNINGS
    C_ONLY
    $<$<CONFIG:Debug>:DEBUG>
    $<$<CONFIG:Release>:NDEBUG>
)

#
# Project options
#
option(QUAKE_BUILD_REF_GL "Builds the RefGL (OpenGL Renderer) module" ON)

# TODO: Include this from a BuildInfo.txt file
set(QUAKE_CLIENT_NAME "quake2")

# TODO: Change quake to not depend on post-fixed DLLs
set(QUAKE_GAME_NAME "game_x64")

#
# Dependencies
#
include(FetchContent)

FetchContent_Declare(
    SDL
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG        2000ccb541fcd4cc22c1d0c91e09926228782b3a
)

FetchContent_MakeAvailable(SDL)

#
# Platform modules
#

# TODO?

#
# Quake modules
#
include(qcommon/CMakeLists.txt)

if (QUAKE_BUILD_REF_GL)
    add_subdirectory(ref_gl)
endif()

#
# Quake client and game
#
add_subdirectory(game)
add_subdirectory(client)