cmake_minimum_required(VERSION 2.8.3)
project(sql_database)

find_package(catkin REQUIRED roscpp)

catkin_package(
  LIBRARIES postgresql_database
  CATKIN_DEPENDS roscpp
  INCLUDE_DIRS database_interface/include
)

include_directories(database_interface/include)

# There's no version hint in the yaml-cpp headers, so get the version number
# from pkg-config.
find_package(PkgConfig REQUIRED)
pkg_search_module(yaml-cpp REQUIRED yaml-cpp)

if(NOT ${yaml-cpp_VERSION} VERSION_LESS "0.5")
add_definitions(-DHAVE_NEW_YAMLCPP)
endif(NOT ${yaml-cpp_VERSION} VERSION_LESS "0.5")

add_subdirectory(database_interface)
add_subdirectory(student_database)
