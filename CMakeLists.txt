cmake_minimum_required(VERSION 3.0.2)
project(autocycle)
find_package(catkin REQUIRED COMPONENTS message_generation roscpp std_msgs)
catkin_python_setup()
add_message_files(FILES
  Object.msg
  LvxPoint.msg
)
add_service_files(FILES
  Lidar.srv
  LvxData.srv
  ObjectList.srv
)
generate_messages(DEPENDENCIES std_msgs)
catkin_package(
  CATKIN_DEPENDS message_runtime std_msgs
)
include_directories(include ${catkin_INCLUDE_DIRS})
add_executable(run_lidar run_lidar.cpp)
add_executable(start_nav start_nav.cpp)
add_executable(parse_lvx parse_lvx.cpp)
target_link_libraries(run_lidar ${catkin_LIBRARIES})
target_link_libraries(run_lidar stdc++fs)
target_link_libraries(start_nav ${catkin_LIBRARIES})
target_link_libraries(parse_lvx ${catkin_LIBRARIES})
catkin_install_python(PROGRAMS bin/bezier_visualization
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
