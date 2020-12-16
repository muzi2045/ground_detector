cmake_minimum_required(VERSION 2.8.3)
project(linefit_ground_segmentation_ros)

set(CMAKE_CXX_COMPILER "/usr/bin/clang++")
set(CMAKE_C_COMPILER "/usr/bin/clang")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -w -O2 ")
# add_definitions(-std=c++11 -g)
find_package(catkin REQUIRED COMPONENTS
    pcl_conversions
    pcl_ros
    roscpp
    rospy
    sensor_msgs
)

catkin_package(
    CATKIN_DEPENDS roscpp
)
find_package(PCL REQUIRED)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

find_package(Eigen3 REQUIRED)
include_directories(${Eigen_INCLUDE_DIRS})
include_directories(${catkin_INCLUDE_DIRS} include)

add_library(linefit_ground_segmentation src/ground_segmentation.cc src/segment.cc src/bin.cc)

add_executable(ground_segmentation_node src/ground_segmentation_node.cc)
# add_executable(ground_segmentation_test_node src/ground_segmentation_test_node.cc)
target_link_libraries(ground_segmentation_node ${catkin_LIBRARIES} ${PCL_LIBRARIES} linefit_ground_segmentation)
# target_link_libraries(ground_segmentation_test_node ${catkin_LIBRARIES} ${PCL_LIBRARIES} linefit_ground_segmentation)


