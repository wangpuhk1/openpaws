
cmake_minimum_required(VERSION 2.8.3)
project(openpaws)

find_package(catkin 
  REQUIRED 
  COMPONENTS
)

catkin_package(
  INCLUDE_DIRS .
)

include_directories(
  .
  ${catkin_INCLUDE_DIRS}
)

install(DIRECTORY .
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".git" EXCLUDE
)
