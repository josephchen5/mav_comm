cmake_minimum_required(VERSION 2.8.3)
project(planning_msgs)

find_package(catkin REQUIRED COMPONENTS geometry_msgs sensor_msgs message_generation mav_msgs trajectory_msgs cmake_modules)
# find_package(Eigen REQUIRED)



include_directories(include ${catkin_INCLUDE_DIRS})

# https://stackoverflow.com/questions/5922016/cmake-cant-find-eigen3
find_package( PkgConfig )
pkg_check_modules( EIGEN3 REQUIRED eigen3 )
include_directories( ${EIGEN3_INCLUDE_DIRS} )

# include_directories(${Eigen_INCLUDE_DIRS})

add_message_files(
  FILES
  Point2D.msg
  PointCloudWithPose.msg
  Polygon2D.msg
  PolygonWithHoles.msg
  PolygonWithHolesStamped.msg
  PolynomialSegment4D.msg
  PolynomialTrajectory4D.msg
)

add_service_files(
  FILES
  PlannerService.srv
  PolygonService.srv
)

generate_messages(
  DEPENDENCIES geometry_msgs sensor_msgs mav_msgs trajectory_msgs
)

catkin_package(
 # INCLUDE_DIRS include ${Eigen_INCLUDE_DIRS}
  INCLUDE_DIRS include ${EIGEN3_INCLUDE_DIRS}
  CATKIN_DEPENDS message_runtime geometry_msgs sensor_msgs mav_msgs trajectory_msgs
)
