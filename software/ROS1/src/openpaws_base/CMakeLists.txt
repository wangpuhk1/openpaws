cmake_minimum_required(VERSION 2.8.3)
project(openpaws_base)

add_compile_options(-std=c++17)

set(CMAKE_BUILD_TYPE Debug)
add_compile_options(-g)

find_package(catkin 
    REQUIRED 
    COMPONENTS 
    roscpp
    rospy
    openpaws_msgs
    visualization_msgs
    geometry_msgs
    sensor_msgs
    trajectory_msgs
    nav_msgs
    tf
    tf2_ros
    urdf
    openpaws
    message_filters
)

catkin_package(
    INCLUDE_DIRS include
    LIBRARIES openpaws_base
    CATKIN_DEPENDS 
    roscpp
    rospy
    openpaws_msgs
    visualization_msgs
    geometry_msgs
    sensor_msgs
    trajectory_msgs
    nav_msgs
    tf
    tf2_ros
    urdf
    message_filters
)

include_directories(
  include
  ${openpaws_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)

install(DIRECTORY config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)

add_library(quadruped_controller src/quadruped_controller.cpp)
add_library(message_relay src/message_relay.cpp)
add_library(state_estimation src/state_estimation.cpp)

add_executable(quadruped_controller_node src/quadruped_controller_node.cpp)
target_link_libraries(quadruped_controller_node quadruped_controller ${catkin_LIBRARIES})
add_dependencies(quadruped_controller_node ${catkin_EXPORTED_TARGETS})
add_dependencies(quadruped_controller ${catkin_EXPORTED_TARGETS})

add_executable(message_relay_node src/message_relay_node.cpp)
target_link_libraries(message_relay_node message_relay ${catkin_LIBRARIES})
add_dependencies(message_relay_node ${catkin_EXPORTED_TARGETS})
add_dependencies(message_relay ${catkin_EXPORTED_TARGETS})

add_executable(state_estimation_node src/state_estimation_node.cpp)
target_link_libraries(state_estimation_node state_estimation ${catkin_LIBRARIES})
add_dependencies(state_estimation_node ${catkin_EXPORTED_TARGETS})
add_dependencies(state_estimation ${catkin_EXPORTED_TARGETS})

install(TARGETS 
    quadruped_controller
    quadruped_controller_node
    message_relay
    message_relay_node
    state_estimation
    state_estimation_node
    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)