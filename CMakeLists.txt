cmake_minimum_required(VERSION 2.8.3)
project(drake_ros_systems)
set(CMAKE_CXX_STANDARD 11)

find_package(drake REQUIRED)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
    std_msgs
    roscpp
)

catkin_package(
  INCLUDE_DIRS include
# CATKIN_DEPENDS message_runtime
#  LIBRARIES perception_msgs
#  CATKIN_DEPENDS other_catkin_pkg
#  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)

include_directories(${catkin_INCLUDE_DIRS})

add_executable(test_ros_publisher_system
    src/test_ros_publisher_system.cc
    include/drake_ros_systems/ros_publisher_system.h)
target_link_libraries(test_ros_publisher_system
	${catkin_LIBRARIES}
    ${drake_LIBRARIES})

add_executable(test_ros_subscriber_system
    src/test_ros_subscriber_system.cc
    include/drake_ros_systems/ros_subscriber_system.h)
target_link_libraries(test_ros_subscriber_system
	${catkin_LIBRARIES}
    ${drake_LIBRARIES})

#############
## Install ##
#############

install(TARGETS test_ros_subscriber_system test_ros_publisher_system
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include/drake_ros_systems/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})