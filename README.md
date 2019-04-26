# project-forming
项目开发需要的构建工具

# Meson
- https://mesonbuild.com
- https://en.wikipedia.org/wiki/Meson_(software)
- https://zh.wikipedia.org/wiki/Meson
- https://github.com/mesonbuild/meson

* Meson语法
> 和python语法相像。Meson变量赋值后不能改变(Meson variables are immutable)，更像常量的概念。不支持自定义函数，所以它不是图灵完整。

```
project('example', 'c')
shared_library('', '')
executable()
```

* 源外构建（out-of-source build）
```
meson setup [builddir] [sourcedir]
```
> 可以省略setup，省略sourcedir时Meson根据当前目录和meson.build文件所在目录来确定。

* 在builddir目录外编译
```
ninja -C builddir
```
* 进入builddir编译
```
cd builddir
ninja
```

# Ninja
- https://ninja-build.org/manual.html
- https://github.com/ninja-build/ninja

* Ninja语法
> 规则不多，目标不是为了方便书写。变量不能修改，可以覆盖

```
cflags = -Wall -Werror

rule cc
  command = gcc $cflags -c $in -o $out

build foo.o: cc foo.c

# 此处的cflags仅为编译special.c时用
build special.o: cc special.c
	cflags = -Wall

# 这里的cc使用外部的cflags
build bar.o: cc bar.c
```

# GCC
- https://gcc.gnu.org

# CMake
- https://cmake.org
- https://cmake.org/cmake-tutorial/
- https://cmake.org/documentation
- https://www.ibm.com/developerworks/cn/linux/l-cn-cmake/
- https://www.jianshu.com/p/bbf68f9ddffa

# Make
- http://www.ruanyifeng.com/blog/2015/02/make.html
- https://www.gnu.org/software/make/manual/make.html

> Make会打印每条命令，然后再执行，可以在命令前加上@，关闭回声效果。

```
1.txt: source.txt
	# 创建文件
	@cat source.txt > 1.txt
```

# Clang+LLVM