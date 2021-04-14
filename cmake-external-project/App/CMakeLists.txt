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
project(hello)

IF( LIBRARY_PATH )
  INCLUDE( ${LIBRARY_PATH}/Libraries_Config.cmake )
ENDIF( LIBRARY_PATH )

if(APPLE)
  if(NOT FLTK_DIR)
    set (FLTK_DIR ${FLTK_INSTALL_DIR}/FLTK.framework/Resources/CMake/
      CACHE PATH
      "FLTK binary folder with FLTKConfig.cmake" FORCE)
  else()
    set (FLTK_DIR ${FLTK_INSTALL_DIR}/FLTK.framework/Resources/CMake/
      CACHE PATH
      "FLTK binary folder with FLTKConfig.cmake")
  endif()
else()
  set (FLTK_DIR ${FLTK_INSTALL_DIR}/share/fltk
      CACHE PATH
      "FLTK binary folder with FLTKConfig.cmake")
endif()

find_package(FLTK CONFIG)

if(FLTK_FOUND)

  add_executable(hello WIN32 MACOSX_BUNDLE ../../src/hello.cxx)

  # This should not be needed if ${FLTK_LIBRARIES} can be used
  if (APPLE)
    target_link_libraries(hello "-framework cocoa")
  endif (APPLE)

  target_include_directories(hello PRIVATE ${FLTK_INCLUDE_DIRS})   # ${FLTK_INCLUDE_DIR} expected

  target_link_libraries(hello fltk)  # ${FLTK_LIBRARIES}

endif()

# Debug ...

message(STATUS "FLTK_INSTALL_DIR            = ${FLTK_INSTALL_DIR}")
message(STATUS "FLTK_DIR                    = ${FLTK_DIR}")
message(STATUS "FLTK_FOUND                  = ${FLTK_FOUND}")
message(STATUS "FLTK_COMMIT                 = '${FLTK_COMMIT}'")
message(STATUS "FLTK_INCLUDE_DIRS           = ${FLTK_INCLUDE_DIRS}")
message(STATUS "FLTK_INCLUDE_DIR            = ${FLTK_INCLUDE_DIR}")
message(STATUS "FLTK_LIBRARIESS             = ${FLTK_LIBRARIES}")
message(STATUS "FLTK_FLUID_EXECUTABLE       = ${FLTK_FLUID_EXECUTABLE}")
message(STATUS "FLTK_WRAP_UI                = ${FLTK_WRAP_UI}")
