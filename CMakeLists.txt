cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

rosbuild_init()

rosbuild_find_ros_package(ontologies)
rosbuild_include(rosprolog utils)

set( OWL_PATH_PREFIX ${ontologies_PACKAGE_PATH} )
fix_ros_destination_path(OWL_PATH_PREFIX)

file(GLOB inputs owl/*.in)

foreach( _in ${inputs} )
  string(REPLACE ".in" "" _out ${_in})
  configure_file( ${_in} ${_out} )
endforeach( _in )

# replace path to local OWL files
rosbuild_find_ros_package(ontologies)
set( LOCAL_PACKAGE_PATH ${ontologies_PACKAGE_PATH} )
fix_ros_destination_path(LOCAL_PACKAGE_PATH)

file(GLOB inputs prolog/*.in)
foreach( _in ${inputs} )
  string(REPLACE ".in" "" _out ${_in})
  configure_file( ${_in} ${_out} )
endforeach( _in )
