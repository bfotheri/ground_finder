cmake_minimum_required(VERSION 2.8.3)
project(ground_finder)
set(CMAKE_CXX_STANDARD 11)

list(APPEND CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake_modules/")

find_package(Eigen3 REQUIRED)
find_package(catkin REQUIRED
  COMPONENTS
    roscpp
    rospy
    std_msgs
    pcl_ros
    pcl_conversions
    sensor_msgs
    octomap_ros
    octomap_msgs
    cmake_modules
)

add_definitions(${EIGEN_DEFINITIONS})

catkin_package(
  CATKIN_DEPENDS std_msgs
  )

include_directories(
    "${PROJECT_SOURCE_DIR}/src/"
    ${catkin_INCLUDE_DIRS}
    ${EIGEN_INCLUDE_DIRS}
    ${EIGEN3_INCLUDE_DIRS}
    )


add_executable(ground_finder src/octomap_ground_extraction.cpp)
target_link_libraries(ground_finder
  ${catkin_LIBRARIES}
)

#############
## Install ##
#############

# Install all the launch files
install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)


# Mark executables and/or libraries for installation
install(TARGETS 
  ground_finder
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
