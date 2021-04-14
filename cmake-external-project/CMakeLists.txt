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
project(hello_top)

add_subdirectory( App )
