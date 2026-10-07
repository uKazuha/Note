# 一、GCC命令的使用



```
gcc命令的使用如下：

gcc [选项] [源文件] [选项] [输出文件]
```

常用参数分类

```
1.编译阶段

-c				仅编译源文件为目标文件(.o),不链接(用于分布编译)
-g				生成调试信息(配合GDB调试)
-Wall			开启所有警告信息(推荐，提前发现代码问题)
-Werror			将警告视为错误(强制修正所有警告)
-00/01/02/03	优化级别(00最低，03最高)
-std=<标准>	   指定C语言标准(-std=c99/-std=c11)	
```





# 二、核心三大文件

## 1.c_cpp_properties.json

代码感知配置文件

**核心作用**：告诉 VSCode 的 C/C++ 插件你的编译器路径、C/C++ 标准、包含目录等信息，用于实现代码的语法检查、智能提示、跳转定义等编辑器功能（不参与编译 / 调试）

```json
{
    "configurations": [
        {
            "name": "Win32",  // 配置名称，可自定义（如MinGW）
            "includePath": [  // 头文件搜索路径，VSCode智能提示会检索这里
                "${workspaceFolder}/**",  // 当前工作区所有目录
                "D:/MinGW/include/**"     // MinGW自带头文件路径（替换为你的路径）
            ],
            "defines": [  // 预定义宏（如DEBUG）
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "D:/MinGW/bin/gcc.exe",  // 编译器路径（gcc/g++）
            "cStandard": "c17",  // C语言标准（c99/c11/c17等）
            "cppStandard": "c++20",  // C++标准（c++11/c++17/c++20等）
            "intelliSenseMode": "windows-gcc-x64"  // 智能提示模式（对应编译器架构）
        }
    ],
    "version": 4
}
```

**关键参数说明**

* ` ${workspaceFolder}`：VSCode 的当前工作区根目录（固定变量，无需修改）；

* `compilerPath`：必须指向你实际安装的`gcc.exe`（Windows）或`gcc`（Linux/Mac）路径，错误会导致智能提示失效；

* `cStandard`：指定使用的 C 语言标准，建议选`c17`（主流兼容）。



## 2.task.json

编译任务配置文件

**核心作用**：定义编译 / 构建任务（如调用 gcc/g++ 编译代码生成可执行文件），是连接 “代码” 和 “可执行文件” 的桥梁。

```json
//支持单文件编译
{
    "version": "2.0.0",
    "tasks": [
        {
            "type": "cppbuild",  // 任务类型（cppbuild为VSCode官方推荐）
            "label": "C/C++: gcc.exe 生成活动文件",  // 任务名称（launch.json会引用）
            "command": "D:/MinGW/bin/gcc.exe",  // 编译命令路径
            "args": [  // 编译参数（传给gcc的参数）
                "-fdiagnostics-color=always",  // 彩色输出编译信息
                "-g",  // 生成调试信息（必须加，否则无法调试）
                "${file}",  // 当前打开的文件（单文件编译）
                "-o",  // 指定输出文件
                "${fileDirname}\\${fileBasenameNoExtension}.exe"  // 输出路径（如：当前目录/文件名.exe）
            ],
            "options": {
                "cwd": "${fileDirname}"  // 编译工作目录（当前文件所在目录）
            },
            "problemMatcher": ["$gcc"],  // 识别gcc的编译错误/警告
            "group": {
                "kind": "build",
                "isDefault": true  // 设置为默认构建任务（Ctrl+Shift+B可直接执行）
            },
            "detail": "编译器: D:/MinGW/bin/gcc.exe"  // 任务描述（可选）
        }
    ]
}
```

**关键参数说明**：

- `-g`：必须添加！该参数让编译器生成调试信息，否则后续`launch.json`调试会失败；
- `${file}`：当前编辑的`.c`文件（比如你打开的`test.c`）；
- `${fileBasenameNoExtension}`：当前文件的 “文件名（不含后缀）”（比如`test.c`对应`test`）。



## 3.launch.json

**核心作用**：定义 “调试指令”，告诉 VSCode 如何调用调试器（如 gdb）运行编译好的可执行文件，支持断点、逐行调试等功能。

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc.exe - 生成和调试活动文件",  // 调试配置名称（可自定义）
            "type": "cppvsdbg",  // 调试器类型（Windows用cppvsdbg，Linux/Mac用lldb）
            "request": "launch",  // 调试模式（launch=启动调试，attach=附加到已有进程）
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",  // 要调试的可执行文件路径（对应tasks.json的输出）
            "args": [],  // 传给程序的命令行参数（比如运行test.exe时传参数，可填["123","456"]）
            "stopAtEntry": false,  // 是否在程序入口（main函数）处自动暂停（false=不暂停）
            "cwd": "${fileDirname}",  // 调试工作目录
            "environment": [],
            "externalConsole": true,  // 是否弹出独立的终端窗口（true=弹出，方便输入输出；false=用VSCode内置终端）
            "MIMode": "gdb",  // 调试器内核（MinGW用gdb）
            "miDebuggerPath": "D:/MinGW/mingw64/bin/gdb.exe",  // gdb路径（替换为你的路径）
            "setupCommands": [
                {
                    "description": "为gdb启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc.exe 生成活动文件"  // 调试前先执行的任务（必须和tasks.json的label一致）
        }
    ]
}
```

**关键参数说明**：

- `preLaunchTask`：必须和`tasks.json`中的`label`完全一致！否则调试时会提示 “找不到预启动任务”；
- `externalConsole`：建议设为`true`，否则 VSCode 内置终端可能无法正常输入（比如`scanf`会失效）；
- `miDebuggerPath`：指向 MinGW 的`gdb.exe`路径，错误会导致调试失败。

