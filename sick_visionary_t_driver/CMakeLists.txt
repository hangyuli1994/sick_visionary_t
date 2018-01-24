cmake_minimum_required(VERSION 2.8.3)
project(sick_visionary_t_driver)

find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  roscpp
  roslaunch
  sensor_msgs
)

find_package(Boost REQUIRED COMPONENTS system)
find_package(OpenCV REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS roscpp sensor_msgs
)

### BUILD ###
include_directories(
  ${catkin_INCLUDE_DIRS}
  include
)

add_executable(sick_visionary_t_driver_node src/node.cpp src/driver.cpp)

target_link_libraries(sick_visionary_t_driver_node
  ${catkin_LIBRARIES}
)

### TEST ###
if(CATKIN_ENABLE_TESTING)
  roslaunch_add_file_check(launch)
endif()

### INSTALL ###
install(TARGETS sick_visionary_t_driver_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
