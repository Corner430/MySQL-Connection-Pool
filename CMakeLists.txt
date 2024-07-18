cmake_minimum_required(VERSION 3.10)
project(MySQLConnectionPool)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 设置库文件输出路径
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# 包含头文件目录
include_directories(${PROJECT_SOURCE_DIR}/include)

# 查找源文件
file(GLOB SOURCES "src/*.cpp")

# 添加动态链接库
add_library(mysql_connection_pool SHARED ${SOURCES})

# 设置输出目录
set_target_properties(mysql_connection_pool PROPERTIES LIBRARY_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH})

# 查找测试代码
file(GLOB EXAMPLE_SOURCES "examples/*.cpp")

# 添加可执行文件
add_executable(example ${EXAMPLE_SOURCES})

# 设置可执行文件的输出目录
set_target_properties(example PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

# 链接动态库
target_link_libraries(example PRIVATE mysql_connection_pool)

target_link_libraries(mysql_connection_pool PRIVATE mysqlclient)

