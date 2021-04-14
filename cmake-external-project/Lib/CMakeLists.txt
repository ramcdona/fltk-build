#
# Example program CMake configuration with CMake module ExternalProject
#
# Author:
#
#   Albrecht Schlosser
#
# CMake Documentation:
#
#   https://cmake.org/cmake/help/latest/module/ExternalProject.html

cmake_minimum_required(VERSION 3.2.3)
project(Libs)

# Edit this as required by your build or change FLTK_COMMIT in the
# CMake cache (e.g. with cmake-gui)

set (FLTK_COMMIT "branch-1.3" CACHE STRING "FLTK branch name, tag, or commit")

set (BUILD_FLTK "${CMAKE_CURRENT_BINARY_DIR}/fltk/${FLTK_COMMIT}")

include(ExternalProject)

ExternalProject_Add(FLTK
    GIT_REPOSITORY      https://github.com/fltk/fltk
    GIT_TAG             "${FLTK_COMMIT}"
    GIT_SHALLOW         TRUE
    PREFIX              ${BUILD_FLTK}/build
    INSTALL_DIR         ${BUILD_FLTK}/bin
    CMAKE_ARGS
                       -DCMAKE_INSTALL_PREFIX=${BUILD_FLTK}/bin
                       -DFLTK_BUILD_TEST=OFF
                       -DFLTK_BUILD_EXAMPLES=OFF
)
ExternalProject_Get_Property( FLTK INSTALL_DIR )
SET( FLTK_INSTALL_DIR ${INSTALL_DIR} )

# Configure file to communicate libraries results to application
configure_file(
   ${CMAKE_SOURCE_DIR}/Libraries_Config.cmake.in
   ${CMAKE_BINARY_DIR}/Libraries_Config.cmake
   @ONLY
)

# Debug ...

message(STATUS "BUILD_FLTK                  = ${BUILD_FLTK}")
