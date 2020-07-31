## Reference1: https://stackoverflow.com/questions/44395859/how-to-use-the-c-library-gtsam-in-my-project-package
##Reference2: https://github.com/raulmur/ORB_SLAM2/issues/494
##Reference3: https://bitbucket.org/gtborg/gtsam/issues/360/couldnt-build-examples, https://github.com/dongjing3309/gtsam-examples

cmake_minimum_required(VERSION 3.0)
project(testGTSAM)

add_compile_options(-std=c++11)

###################################

# Include GTSAM CMake tools
find_package(GTSAMCMakeTools)
#include(GtsamBuildTypes) # Load build type flags and default to Debug mode
#include(GtsamTesting)    # Easy functions for creating unit tests and scripts
#include(GtsamMatlabWrap) # Automatic MATLAB wrapper generation

# Ensure that local folder is searched before library folders
#include_directories(BEFORE "${PROJECT_SOURCE_DIR}")

# Find GTSAM components
find_package(GTSAM REQUIRED) # Uses installed package
include_directories(${GTSAM_INCLUDE_DIR})

# Build static library from common sources
#set(CONVENIENCE_LIB_NAME ${PROJECT_NAME})
#add_library(${CONVENIENCE_LIB_NAME} STATIC include/car/car_lib.h src/car_lib.cpp)
#target_link_libraries(${CONVENIENCE_LIB_NAME} gtsam)

###################################


## Create a C++ library/object file for all the user source files
add_library(odomLib src/OdometryExample.cpp)

## Attach/Link gtsam to this library
target_link_libraries(odomLib
  gtsam)

## Create the actual exe file for the given source files
add_executable(gtsamExe src/OdometryExample.cpp)

## Attach/Link user/source libs to this exe
target_link_libraries(gtsamExe
  odomLib)
