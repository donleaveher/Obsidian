## CMake 配置
- ### C++编译原理
	- #### 1. 预处理
		在这个阶段，编译器会
		- 处理所有的预处理指令（如 `#include`、`#define`、`#ifdef` 等）
		- 展开所有的宏定义
		- 删除注释
		- 包含所有的头文件
```Cmake.text
# 标题
cmake_minimum_required(VERSION 3.5.0)
project(SDLShooter VERSION 0.1.0 LANGUAGES C CXX)

# 查找并载入Cmake预设
find_package(SDL2 REQUIRED)

# 添加可执行文件
add_executable(SDLShooter main.cpp)

# 链接库
target_link_libraries(SDLShooter 
                        SDL2::SDL2 
                        SDL2::SDL2main)

```
- **cmake_minimum_required**：指定构建项目所需的最低CMake版本
- **project**：定义项目名称、版本和使用的编程语言
- **find_package**：查找并加载SDL2库的CMake配置
- **add_executable**：指定要构建的可执行文件及其源代码文件
- **target_link_libraries**：指定要链接的库

## SDL基础框架
初始化 -- 创建窗口 -- 创建渲染器 -- ······ -- 释放渲染器 -- 释放窗口 -- 退出
![[Pasted image 20250913030953.png]]