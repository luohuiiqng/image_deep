cmake_minimum_required(VERSION 3.14) # 更现代的版本
set(CMAKE_CXX_STANDARD 17)
project(PCLExample)

# 查找依赖
find_package(Freetype REQUIRED)
find_package(JsonCpp REQUIRED)
# find_package(Vulkan REQUIRED)
find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(PCL REQUIRED OMPONENTS
    common
    io
    geometry
    kdtree        # 提供 KdTree 和 FLANN 支持
    search        # 搜索树相关
    features      # FPFH、法线等特征提取
    )
# find_package(PCL 1.12 REQUIRED COMPONENTS common io visualization)
include_directories(${EIGEN3_INCLUDE_DIR})
include_directories(${OpenCV_INCLUDE_DIRS})
include_directories(${PCL_INCLUDE_DIRS})

# 添加可执行文件
aux_source_directory(${CMAKE_SOURCE_DIR}/src DIR_SRCS)
include_directories(${CMAKE_SOURCE_DIR}/include)
add_executable(pcl_example ${DIR_SRCS})

# 链接库（现代 CMake 推荐使用 target_link_libraries）
target_link_libraries(pcl_example
    PRIVATE
        ${OpenCV_LIBS}
        ${PCL_LIBS}
)
message(STATUS "Eigen include dir: ${EIGEN3_INCLUDE_DIR}")
message(STATUS "OpenCV_INCLUDE_DIR include dir: ${OpenCV_INCLUDE_DIRS}")
message(STATUS "PCL_INCLUDE_DIRS include dir: ${PCL_INCLUDE_DIRS}")

