if(("$ENV{ROS_DISTRO}" STREQUAL "indigo") OR ("$ENV{ROS_DISTRO}" STREQUAL "jade"))
else()

  include(CheckCXXCompilerFlag)
  CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
  if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  else()
    message(STATUS  "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
  endif(COMPILER_SUPPORTS_CXX11)

  find_package(Eigen3 REQUIRED)
  include_directories(${Eigen_INCLUDE_DIRS})
endif()
add_library(object_information_cache info_cache.cpp)
target_link_libraries(object_information_cache ${catkin_LIBRARIES})

install(TARGETS object_information_cache
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
