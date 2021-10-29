cmake_minimum_required(VERSION 3.4)
project(qp_oases)

# C++17
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# find catkin and any catkin packages
find_package(
	catkin REQUIRED
	COMPONENTS
		roscpp
)

# declare a catkin package
catkin_package(
	INCLUDE_DIRS
		include
	LIBRARIES
		qp_oases
	CATKIN_DEPENDS
		roscpp
)

# additional locations of header files
include_directories(
	include
	${catkin_INCLUDE_DIRS}
)

################################################################################################

# libraries
# REMEMBER TO ADD TO INSTALL TARGETS (bottom of file) !!!

## qp_oases
FILE(GLOB QP_OASES_SRC src/*.cpp)
add_library(qp_oases ${QP_OASES_SRC})
target_link_libraries(qp_oases ${catkin_LIBRARIES})

##############################################################

# node
add_executable(example1 examples/example1.cpp)
target_link_libraries(example1 ${catkin_LIBRARIES} qp_oases)

################################################################################################

# install targets

## executables and/or libraries for installation
install(
	TARGETS
		qp_oases
	ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
)

## install header files
install(
	DIRECTORY
		include/qp_oases/
	DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)