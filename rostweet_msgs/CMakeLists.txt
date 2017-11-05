cmake_minimum_required(VERSION 2.8.3)
project(rostweet_msgs)

## Project dependencies
find_package(catkin REQUIRED COMPONENTS
  message_generation
  sensor_msgs
)

################################################
## Declare ROS messages, services and actions ##
################################################

## Generate messages in the 'msg' folder
add_message_files(
  FILES
  IncomingTweet.msg
)

## Generate services in the 'srv' folder
add_service_files(
  FILES
  postTweet.srv
)

## Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
  sensor_msgs
)

###################################
## catkin specific configuration ##
###################################

catkin_package(
  CATKIN_DEPENDS
    message_runtime
    sensor_msgs
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
  ${catkin_INCLUDE_DIRS}
)

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

install(
  DIRECTORY "include/std_msgs/"
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  PATTERN "*.h"
)

