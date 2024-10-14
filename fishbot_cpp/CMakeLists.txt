cmake_minimum_required(VERSION 3.8)
project(fishbot_cpp)

# 设置策略 CMP0115
# cmake_policy(SET CMP0115 NEW)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# 查找依赖项
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(nav2_msgs REQUIRED)

# 添加可执行文件
add_executable(nav2_topose src/nav2_topose.cpp)

# 依赖项
ament_target_dependencies(nav2_topose rclcpp rclcpp_action nav2_msgs)

# 如果需要测试
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # 跳过版权检查（如果添加了版权和许可，可以取消注释）
  set(ament_cmake_copyright_FOUND TRUE)
  # 跳过 cpplint 检查（如果在 Git 仓库中并添加了版权和许可，可以取消注释）
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

# 安装目标
install(TARGETS 
  nav2_topose
  DESTINATION lib/${PROJECT_NAME}
)

# 生成包信息
ament_package()