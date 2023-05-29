# g++

## G++的重要编译参数

**-g**

作用: 高数GCC产生能被 GNU 调试器GDB使用的信息，以便调试程序。

使用：

g++ -g test.cpp -o test

-o

种类：

-O  主要进行跳转和延迟退栈两种优化；
-O2 除了完成-O1的优化之外，还进行一些额外的调整工作，如指令调整等。
-O3 则包括循环展开和其他一些与处理特性相关的优化工作。
选项将使编译的速度比使用 -O 时慢， 但通常产生的代码执行速度会更快。
作用：告诉 GCC 对源代码进行基本优化告诉 GCC 对源代码进行基本优化。

使用：g++ -o2 test.cpp -o test
-I

作用：

用来指定头文件目录。/usr/include目录一般是不用指定的，gcc知道默认去/usr/include找，但 是如果头文件不在/usr/icnclude里我们就要用-I参数指定了，比如头文件放在/myinclude目录里，那编译命令行就要加上-I/myinclude参数了，如果不加你会得到一个"xxxx.h: No such file or directory"的错误。

使用：g++ -I/myinclude test.cpp

 **-Wall**

 作用：打印出gcc提供的警告信息

使用：g++ -wall test.cpp

**-std=c++11**

作用：使用c++11标准编译

使用：g++ -std=C++11 test.cpp

**-o**

作用：指定输出文件名，不加参数默认生成a.out文件

# cmake

编写CMakeLists.txt，可以帮助生成工程项目，

会生成一个build目录，在目录下cmake ..编译，mingw32-make.exe,就生成了目标文件。如果安装过VS，可能会调用msvc编译器，使用（cmake -G "MinGW Makefiles" ..）代替cmake..

## 常用命令

EG:

cmake -B [构建书目录] -S [源码目录] -D CMAKE_BUILD_TYPE=Debug(Release)

cmake --build [目录] //生成exe

cmake -G [选择构建器] 

执行一个cmake脚本

cmake -P xxx.cmake

**在 CMake 中，`**include**` 命令用于将指定的外部 CMake 脚本文件引入当前的 CMakeLists.txt 文件中**

`**add_subdirectory**` 是 CMake 中的一个命令，用于向当前项目添加一个子目录，并在该子目录中执行一个新的 CMakeLists.txt 文件

`**target_include_directories**`用于向一个或多个目标添加头文件搜索路径。

以上两个配合使用在构建项目时eg：文档cmake入门3

```
**target_link_libraries**用于为目标添加链接库或者链接其他目标。
```

add_executable用于将源代码文件编译成可执行文件

add_library（添加库）函数用于创建静态或共享库。

**别名目标**：允许为现有的目标创建一个不同的名称。eg：

add_library(mylib STATIC mylib.cpp) #定义了一个mylib的库目标

add_library(my::lib ALTAS mylib )#创建了一个别名

可以使用：target_link_libraries(mycpp PRIVATE my::lib)

## find_package （详细见cmake入门07）

使用第三方库，主要是找到头文件、库文件、目标，有两种模式 

查找包的流程：

通常，find模块按照以下顺序执行:

\1.   它查找属于包的文件。

\2.   它设置包含包的【包含】目录和【库目录】的变量。

\3.   它为导入的包设置了目标Target。

\4.   它为目标Target设置属性。

### module 

CMake搜索名为Find<PackageName>.cmake的文件

首先在CMAKE_MODULE_PATH中列出的位置中查找，然后在CMake安装提供的Find模块中查找。

### config

find_package()使用CONFIG 模式查找：

<CamelCasePackageName>Config.cmake 使用驼峰式命名法

<kebab-case-package-name>-config.cmake 使用烤串式命名法

 如果系统下有这两类文件，表示通过CONFIG 找到了

### 查找结果

您可以期望在调用 find_package() 时设置一些变量，无论您使用的是内置查找模块还是与包捆绑在一起的配置文件（假设已找到包）：

<PKG_NAME>_FOUND 查找结果；

<PKG_NAME>_INCLUDE_DIRS or <PKG_NAME>_INCLUDES 头文件；

<PKG_NAME>_LIBRARY or <PKG_NAME>_LIBRARIES or <PKG_NAME>_LIBS 库文件；

<PKG_NAME>_DEFINITIONS

IMPORTED targets specified by the find-module or config-file 由查找模块或配置文件指定的导入目标

### 使用 FindPkgConfig 发现旧版包-过时的方法

要求CMake用find_package()命令找到PkgConfig可执行文件

### 自己编写查找模块(未学会)

# task.json launch.json

注意工程路径要一致，先编译在调试，不然调试的是上次编译的，咋launch中有个字段可指定调试前生成工程的任务，preLaunchTaks;

可以将使用cmake编译时的操作，卸载task中，每次调试就不用一直输入cmake的相关命令；(需要在编写好CMakeLists文件之后，并创建build目录之后，)

# vcpkg

[vcpkg/README_zh_CN.md at master · microsoft/vcpkg (github.com)](https://github.com/microsoft/vcpkg/blob/master/README_zh_CN.md#visual-studio-cmake-工程中使用-vcpkg)