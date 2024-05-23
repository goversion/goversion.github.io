# gdb 的全景使用

## 安装 riscv64-unknown-elf-gdb
1. 安装依赖（针对 Linux，macOS 可以遇到错误再去搜索）

python 并非必须
在 Ubuntu 20.04 等系统中，python 和 python-dev 需要替换成 python2 和 python2-dev
sudo apt-get install libncurses5-dev python python-dev texinfo libreadline-dev
2. 前往清华镜像下载最新的 GDB 源代码

3. 执行以下命令

--prefix 是安装的路径，按照以上指令会安装到 /usr/local/bin/ 下
--with-python 是 python2 的地址，它和 --enable-tui 都是为了支持后续安装一个可视化插件，并非必须
```
mkdir build
cd build
../configure --prefix=/usr/local --with-python=/usr/bin/python --target=riscv64-unknown-elf --enable-tui=yes
```

4. 编译安装
```
make -j$(nproc)
sudo make install
```

## GDB 命令

make debug MODE=debug LOG=INFO
- tui layout src
- b <funcName>: 添加断点
- c: 继续运行, 遇到断点会中断
- s: 执行下一行代码，进入函数
- n: 执行下一行代码, 不进入函数
- info reg
- finish：结束当前函数，返回到函数调用点
- ni/si：是执行一条汇编指令，不是执行一条rust语句


## 设断点
通过 `info functions` 找到main 符号。
```
(gdb) info function run_next_app
(gdb) b os::batch::run_next_app
```

## 安装 gdb-dashboard 插件，优化 debug 体验

wget -P ~ https://git.io/.gdbinit

## 接下来要做的事

![](/pics/os/2_03.png)

见上图，通过 si 不能进入汇编语言 __restore，原因在哪里？

有空时，专门练习一下汇编语言GDB的调试办法。

## 参考：
- https://www.cnblogs.com/bonelee/p/13759115.html