# cmake version
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

SET(CMAKE_CXX_COMPILER g++)

# release option
SET(CMAKE_CXX_FLAGS_RELEASE "-Wall -O2 -fpermissive")
# debug option
SET(CMAKE_CXX_FLAGS_DEBUG "-g -fpermissive")

# build type
SET(CMAKE_BUILD_TYPE Release)
#set(CMAKE_BUILD_TYPE Debug)

# project name
PROJECT(getCalibDataDS325)

FIND_PACKAGE(OpenCV REQUIRED)
#FIND_PACKAGE(Boost)
#find_package(OpenMP)
#find_package(OpenGL)
#find_package(GLUT)
#if (OPENMP_FOUND)
#    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
#    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
#endif()

# include dir
INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/include")
INCLUDE_DIRECTORIES(/opt/softkinetic/DepthSenseSDK/include)

# library dir
LINK_DIRECTORIES("/usr/local/lib")
LINK_DIRECTORIES("/usr/lib")
LINK_DIRECTORIES("/opt/softkinetic/DepthSenseSDK/lib")

ADD_EXECUTABLE(getCalibDataDS325 ./src/main.cpp)
TARGET_LINK_LIBRARIES(getCalibDataDS325 DepthSense DepthSensePlugins turbojpeg ${OpenCV_LIBRARIES} gflags)

