cmake_minimum_required(VERSION 2.8 FATAL_ERROR)
set (CMAKE_CXX_STANDARD 11)

SET_PROPERTY(GLOBAL PROPERTY TARGET_SUPPORTS_SHARED_LIBS TRUE)

IF(WIN32 OR win64)
   SET(CMAKE_FIND_LIBRARY_SUFFIXES .lib .dll)
ELSE()
   SET(CMAKE_FIND_LIBRARY_SUFFIXES .a)
ENDIF()

project(ConvertDeps)

find_package( OpenCV REQUIRED )
 
include_directories(C:/opencv/build)
include_directories(${ConvertDeps_SOURCE_DIR})

file(GLOB_RECURSE ConvertDeps_HEADERS *.h)
file(GLOB_RECURSE ConvertDeps_SOURCES *.cpp)
set (ConvertDeps_INCLUDE_DIRS "")
foreach (_headerFile ${ConvertDeps_HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND ConvertDeps_INCLUDE_DIRS ${_dir})
endforeach()
list(REMOVE_DUPLICATES ConvertDeps_INCLUDE_DIRS)

include_directories(${ConvertDeps_INCLUDE_DIRS})


add_executable (ConvertDeps ConvertDeps.cpp)
target_link_libraries (ConvertDeps ${OpenCV_LIBS})
