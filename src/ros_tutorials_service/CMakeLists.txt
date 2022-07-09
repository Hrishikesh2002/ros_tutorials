cmake_minimum_required(VERSION 2.8.3)
project(ros_tutorials_service)
## A component package required when building the Catkin.
## Has dependency on message_generation, std_msgs, roscpp.
## Error occurs during the build if these packages are missing.
find_package(catkin REQUIRED COMPONENTS message_generation std_msgs roscpp)
## Serivce Declaration: SrvTutorial.srv
add_service_files(FILES SrvTutorial.srv)
## Configure the dependent message.
## An error occurs duing the build if "std_msgs" is not installed.
generate_messages(DEPENDENCIES std_msgs)
## A Catkin package option that describes the library, the Catkin build
## dependencies, and the system dependent packages.
catkin_package(
LIBRARIES ros_tutorials_service
CATKIN_DEPENDS std_msgs roscpp
)
## Configure the directory to Include
include_directories(${catkin_INCLUDE_DIRS})
## Build option for the "service_server" node.
## Configuration of Executable files, target link libraries, and additional
## dependencies.
add_executable(service_server src/service_server.cpp)
add_dependencies(service_server ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(service_server ${catkin_LIBRARIES})
## Build option for the "service_client" node.
add_executable(service_client src/service_client.cpp)
add_dependencies(service_client ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(service_client ${catkin_LIBRARIES})