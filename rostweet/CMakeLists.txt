cmake_minimum_required(VERSION 2.8.3)

project(rostweet)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find ROS compile-time dependencies
find_package(catkin REQUIRED COMPONENTS
  cmake_modules
  roslib
  roscpp
  cv_bridge
  rostweet_msgs
)

## Find system dependencies
find_package(CURL REQUIRED)
find_package(TinyXML REQUIRED)

###################################
## catkin specific configuration ##
###################################

catkin_package(
  CATKIN_DEPENDS
    roslib
    roscpp
    cv_bridge
    rostweet_msgs
  DEPENDS
    CURL
    TinyXML
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(
  ${catkin_INCLUDE_DIRS}
  ${CURL_INCLUDE_DIRS}
  ${TinyXML_INCLUDE_DIRS}
)

## Add cmake target dependencies of the library
## as an example, code may need to be generated before libraries
## either from message generation or dynamic reconfigure
# add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
add_executable(${PROJECT_NAME}_bridge
  "src/rostweet_bridge.cpp"
  "src/HMAC_SHA1.cpp"
  "src/SHA1.cpp"
  "src/base64.cpp"
  "src/oauthlib.cpp"
  "src/twitcurl.cpp"
  "src/urlencode.cpp"
)

## Rename C++ executable without prefix
## The above recommended prefix causes long target names, the following renames the
## target back to the shorter version for ease of user use
## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
set_target_properties(${PROJECT_NAME}_bridge PROPERTIES OUTPUT_NAME bridge PREFIX "")

## Specify libraries to link a library or executable target against
target_link_libraries(${PROJECT_NAME}_bridge
  ${catkin_LIBRARIES}
  ${CURL_LIBRARIES}
  ${TinyXML_LIBRARIES}
)

#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

install(TARGETS ${PROJECT_NAME}_bridge
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_rostweet_bridge.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)

