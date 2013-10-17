# CMakeのバージョン
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

SET(CMAKE_CXX_COMPILER g++)

# リリースビルド用オプション
SET(CMAKE_CXX_FLAGS_RELEASE "-Wall -O2 -fpermissive")
# デバッグビルド用オプション
SET(CMAKE_CXX_FLAGS_DEBUG "-g -fpermissive")
# ビルドのタイプはリリース
SET(CMAKE_BUILD_TYPE Release)
#set(CMAKE_BUILD_TYPE Debug)

#set(CMAKE_CXX_FLAGS "$(CMAKE_CXX_FLAGS) -fpermissive")

# プロジェクト名
PROJECT(HFMD_softkinetic)

FIND_PACKAGE(OpenCV REQUIRED)
FIND_PACKAGE(Boost)
find_package(OpenMP)
#find_package(OpenGL)
#find_package(GLUT)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

# バージョン番号
SET(serial "1.0.0")
# 共有ライブラリのバージョン番号
SET(soserial "1")
# ビルドするためにインクルードするヘッダーファイルの場所
INCLUDE_DIRECTORIES("${PROJECT_SOURCE_DIR}/include")
INCLUDE_DIRECTORIES(/opt/softkinetic/DepthSenseSDK/include)

# ライブラリの場所
LINK_DIRECTORIES("/usr/local/lib")
LINK_DIRECTORIES("/usr/lib")
LINK_DIRECTORIES("/opt/softkinetic/DepthSenseSDK/lib")

# 共有ライブラリとしてビルド
#ADD_LIBRARY(HFMD_core SHARED src/CConfig.cpp src/CRForest.cpp src/HoG.cpp src/CDataset.cpp src/CRTree.cpp src/util.cpp)
ADD_EXECUTABLE(HFMD_softkinect ConsoleDemo.cxx)

#TARGET_LINK_LIBRARIES(HFMD_softkinect  ${Boost_LIBRARIES} DepthSense DepthSensePlugins turbojpeg ${OpenCV_LIBRARIES} opencv_core opencv_imgproc opencv_highgui opencv_ml opencv_video opencv_features2d opencv_calib3d opencv_objdetect opencv_contrib opencv_legacy opencv_flann)
TARGET_LINK_LIBRARIES(HFMD_softkinect HFMD_core ${Boost_LIBRARIES} DepthSense DepthSensePlugins turbojpeg ${OpenCV_LIBRARIES})

