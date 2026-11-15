# CMake

#### 1.CMake是什么

CMake 是一个跨平台的项目构建工具。

它主要帮助我们管理 C/C++ 项目，告诉编译器：

- 哪些源代码文件需要编译？
- 使用什么编译标准？
- 头文件在哪里？
- 需要链接哪些库？
- 如何生成可执行程序？
- 如何执行自动化测试？

**简单理解：CMake 帮助我们管理整个项目的编译过程**

#### 2.为什么需要CMake

假设我们有一个简单的 C 项目：

```text
MyProject/
├── main.c
├── add.c
├── add.h
├── sub.c
└── sub.h
```

如果不使用 CMake，我们可能需要手动输入：

```bash
gcc main.c add.c sub.c -o MyProject
```

当项目文件越来越多时，手动管理编译命令就会越来越麻烦。

使用 CMake 后，我们只需要编写一次 `CMakeLists.txt`，之后就可以使用统一命令构建项目：

```bash
cmake -S . -B build
cmake --build build
```

第一条

| 参数    | 含义                      |
| ------- | ------------------------- |
| `cmake` | 调用 CMake 程序           |
| `-S`    | 指定源代码目录（Source）  |
| `.`     | 当前目录                  |
| `-B`    | 指定构建目录（Build）     |
| `build` | 把构建文件放到 build 目录 |

所以整条命令的意思是：

**读取当前目录中的 CMakeLists.txt，分析项目配置，并在 build 目录中生成构建所需的文件。**

第二条

| 参数    | 含义         |
| ------- | ------------ |
| cmake   | 调用CMake    |
| --build | 执行构建     |
| build   | 指定构建目录 |

意思是：

**让 CMake 使用 build 目录中已经生成的构建配置，调用对应的编译工具来编译项目。**

#### 3.CMake和GCC区别

| 工具    | 作用                        |
| ------- | --------------------------- |
| VS Code | 编写和管理代码              |
| CMake   | 管理项目构建过程            |
| GCC     | 编译 C 语言代码             |
| Make    | 根据 Makefile 执行构建      |
| Ninja   | 根据 Ninja 构建文件执行构建 |
| GDB     | 调试程序                    |

CMake 本身不是编译器，真正编译 C 代码的是 GCC、Clang 等编译器

#### 4.常见操作

删除构建目录：

`rm -rf build`

重新配置：

`cmake -S . -B build`

重新编译：

`cmake --build build`

清理后重新编译：

`cmake --build build --clean-first`

#### 5.CMake常用命令

| 命令                         | 作用               |
| ---------------------------- | ------------------ |
| cmake_minimum_required()     | 指定最低版本       |
| project()                    | 定义项目           |
| set()                        | 设置变量           |
| add_executable()             | 创建可执行文件     |
| add_library()                | 创建库             |
| target_include_directories() | 指定头文件搜索目录 |
| target_link_libraries()      | 链接库             |
| add_subdirectory()           | 添加子目录         |
| add_test()                   | 添加测试           |
| enable_testing()             | 启用测试           |
| find_package()               | 查找外部依赖       |
| option()                     | 定义可配置选项     |
| add_custom_target()          | 创建自定义构建目标 |

#### 6.使用Ninja构建项目

除了Make，CMake还支持Ninja。

使用命令：

`cmake -S . -B build-ninja -G Ninja`

编译：

`cmake --build build-ninja`

#### 7.CMake实际开发工作流程

1.了解项目结构

`ls`

查看有没有：

`CMakeLists.txt`

如果有，说明项目已经提供了CMake构建配置。

2.配置项目

`cmake -S . -B build`

3.编译项目

`cmake --build build`

4.执行测试

`ctest --test-dir build --output-on-failure`

5.运行程序

根据项目生成的可执行文件位置执行：

`./build/程序名称`

