cmake_minimum_required(VERSION 3.5)
project(mavros_msgs)

find_package(ament_cmake REQUIRED)

find_package(builtin_interfaces REQUIRED)
find_package(geographic_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(std_msgs REQUIRED)

find_package(rosidl_default_generators REQUIRED)

# Generate msg and srv file lists
file(GLOB msg_files
  RELATIVE ${CMAKE_CURRENT_LIST_DIR}
  msg/*.msg
)
file(GLOB srv_files
  RELATIVE ${CMAKE_CURRENT_LIST_DIR}
  srv/*.srv
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  DEPENDENCIES geographic_msgs geometry_msgs sensor_msgs std_msgs
)

ament_export_dependencies(
  geographic_msgs
  geometry_msgs
  sensor_msgs
  std_msgs
)

ament_export_include_directories(
  include
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
  FILES_MATCHING PATTERN "*.h"
)

ament_package()