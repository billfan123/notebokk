from https://zhuanlan.zhihu.com/p/419549598

在根目录下，新建目录 build 并且进入该目录，在 build 目录下，通过指定上级目录的 CMakeLists.txt 来调用 CMake 配置项目并生成构建器

mkdir -p build
cd build
cmake ..
# or specify a generator available the platform
cmake .. -G "MinGW Makefiles"

编译项目
随后就可以开始编译可执行文件

make
# or
cmake --build .

打开窗口错误后，发现是asset文件没有设置，修改asset路径后就可以打开