# gcc五分钟系列
## 第十七节：库的使用（一）：使用

### c与zip
半年以前的事情了。
有一次，我在一个C项目中需要读写zip压缩包文件。很幸运地，我发现了libzip库。[http://packages.debian.org/squeeze/libzip-dev]
然后，一切问题就都解决了。
咋解决的？听我慢慢道来。

### 库
编程中，有一件很神奇的事情，叫做 _复用_ 。通常，我们将一个功能封装在一个函数中，目的是为了以后遇见相同功能的时候，不需要把这个函数再写一遍。
可是，函数级别的复用有时候会显得力不从心。因此，出现了 __库__ 技术。
库的优点有很多，例如：
* 它是编译好的二进制文件，体积小，不需要用户自己编译。
* 发布简单。使用方便。

通常，库根据链接方式的不同，分为两种：静态链接和动态链接。这里我们先介绍动态链接的方法。

### 使用libzip
我写了一个简单的程序，zipdemo，它的目的是输出一个zip包里的文件列表。
使用libzip，一共分为三步。
#### 1.安装libzip。

	sudo apt-get install libzip-dev

这里需要注意一下，软件包libzip包含的是运行时库，而我们需要的是开发库，也就是libzip-dev。
#### 2.编写源代码，使用libzip中的函数。
##### 2.1.首先要包含头文件。

	#include <zip.h>

##### 2.2.使用libzip中的函数。
函数的列表及每个函数的详细介绍可以在libzip的man手册中找到。
#### 3.编译链接。
##### 3.1.由于zip.h头文件是放在/usr/include下的，因此不需要显式地指定include目录。编译的步骤没有任何区别。

	gcc -c -o zipdemo.o zipdemo.c

##### 3.2.链接时，需要指定链接的动态库的名字。这里我们使用-l参数。

	gcc -lzip -o zipdemo zipdemo.o

zipdemo源代码及Makefile可以参见本项目git仓库。

### 本节完

> 附1.从本节起，本系列改用markdown语法，使用github.com的markdown解释器。
本项目的github.com地址为：[https://github.com/lexdene/gcc_five_minute]。
本项目的51cto.com专题地址为：[http://blog.51cto.com/zt/229]

> 附2.其实 _debian_ 的软件仓库里面基本上已经涵盖了我们需要的各类编程库，尤其以C库居多。
每次当我需要某功能的时候，我都会先在 _debian_ 的软件仓库中搜索一下，有没有已经提供的库。
搜索地址：[http://www.debian.org/distrib/packages]
