cmake_minimum_required(VERSION 3.16.3)
project(qp_oases)

# C++17
set(CMAKE_CXX_STANDARD 17)

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

# include directories
include_directories(
	include
	${catkin_INCLUDE_DIRS}
)

################################################################################################

# libraries

FILE(GLOB SRC src/*.cpp)

## ur5_controller
add_library(qp_oases ${SRC})
target_link_libraries(qp_oases ${catkin_LIBRARIES})

install(
	TARGETS qp_oases
	ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
	RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
)

## install all project namespaced headers (package/include)
install(
	DIRECTORY include/${PROJECT_NAME}/
	DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

##############################################################

# node
add_executable(example1 examples/example1.cpp)
target_link_libraries(example1 ${catkin_LIBRARIES} qp_oases)