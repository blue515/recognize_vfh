cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

# we need FindFLANN.cmake 
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR})

project(recognize_object)

find_package(PCL 1.2 REQUIRED)
include_directories(${PCL_INCLUDE_DIRS} ./)
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

find_package(HDF5)
if(HDF5_FOUND)

  find_package(FLANN)
  include_directories(${FLANN_INCLUDE_DIRS})

  include_directories(${HDF5_INCLUDE_DIR})

  add_executable(recognize_object recognize_object.cpp)
  target_link_libraries(recognize_object ${PCL_LIBRARIES} ${Boost_LIBRARIES}
                                 ${FLANN_LIBRARIES} ${HDF5_hdf5_LIBRARY})
  #ORB-SLAM3中
  target_link_libraries(${PROJECT_NAME} mpi_cxx)
  link_libraries("/usr/lib/x86_64-linux-gnu/libmpi_cxx.so.20")

endif(HDF5_FOUND)
