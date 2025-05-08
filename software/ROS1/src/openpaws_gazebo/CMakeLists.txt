
cmake_minimum_required(VERSION 2.8.3)
project(openpaws_gazebo)

add_compile_options(-std=c++17)

find_package(gazebo REQUIRED)

find_package(catkin 
  REQUIRED 
  COMPONENTS
  roscpp
  urdf
  openpaws
  openpaws_msgs
)

catkin_package(
   CATKIN_DEPENDS 
   roscpp
)

install(PROGRAMS
  scripts/imu_sensor.py
  scripts/odometry_tf.py
  scripts/odometry.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

include_directories(
  include
  ${openpaws_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
  ${PROJECT_SOURCE_DIR}/../openpaws
)

link_directories(${GAZEBO_LIBRARY_DIRS} ${catkin_LIBRARIES})
add_compile_options("${GAZEBO_CXX_FLAGS}")

add_executable(contact_sensor src/contact_sensor.cpp)
target_link_libraries(contact_sensor ${GAZEBO_LIBRARIES} pthread ${catkin_LIBRARIES} )
add_dependencies(contact_sensor ${catkin_EXPORTED_TARGETS})

install(TARGETS 
    contact_sensor
    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

install(DIRECTORY worlds/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/worlds
)
