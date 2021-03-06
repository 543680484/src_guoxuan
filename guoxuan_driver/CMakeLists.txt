cmake_minimum_required(VERSION 2.8.3)
project(guoxuan_driver)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3 -std=c++11 -fPIC")

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS roscpp rospy std_msgs geometry_msgs tf genmsg dynamic_reconfigure)
#find_package(Eigen3 REQUIRED)

include_directories(${catkin_INCLUDE_DIRS}
${EIGEN3_INCLUDE_DIRS}
include
/usr/include/eigen3)

add_definitions(${EIGEN3_DEFINITIONS})

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
  roscpp
  geometry_msgs
  message_runtime
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

#file(GLOB HEADER_FILES include/*.h)

include_directories(include)

link_directories(${EIGEN3_LIBRARY_DIRS})

add_executable(magnetic_driver_hinson src/magnetic_driver_hinson.cpp ${HEADER_FILES})
target_link_libraries(magnetic_driver_hinson ${catkin_LIBRARIES})
add_dependencies(magnetic_driver_hinson ${PROJECT_NAME}_generate_messages_cpp)

add_executable(sound_player_driver src/sound_player_driver.cpp ${HEADER_FILES})
target_link_libraries(sound_player_driver ${catkin_LIBRARIES})
add_dependencies(sound_player_driver ${PROJECT_NAME}_generate_messages_cpp)

add_executable(magnetic_tf_pub src/magnetic_tf_pub.cpp)
target_link_libraries(magnetic_tf_pub ${catkin_LIBRARIES})# ${CERES_LIBRARIES})
add_dependencies(magnetic_tf_pub ${PROJECT_NAME}_generate_messages_cpp)
#        ${artoolkit_EXPORTED_TARGETS})
