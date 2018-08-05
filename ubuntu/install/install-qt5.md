安装
首先在qt官网下载 qt-opensource-linux-x64-5.10.0.run,网址如下： 
http://download.qt.io/archive/qt/ 
在Ubuntu中使用chmod命令给该文件添加x权限并运行，如下：

$ chmod a+x  qt-opensource-linux-x64-5.10.0.run
$ ./qt-opensource-linux-x64-5.10.0.run
1
2
3
安装后的配置
之后按照提示安装完毕，由于Qt5包含了qtcreator集成开发环境，如果想自己通过qmake编译，需要进行一些设置。

1.首先在/usr/share/qtchooser/目录中添加一个default文件，如果没有qtchooser目录，则先通过apt install qtchooser进行安装，default文件内容如下：

/opt/Qt5.10.0/5.10.0/gcc_64/bin
1
/opt/Qt5.10.0/5.10.0/
2
3
2.配置PATH环境变量。在~/.bashrc中加入一行，内容如下：

PATH=${PATH}:/opt/Qt5.10.0/5.10.0/gcc_64/bin:/opt/Qt5.10.0/Tools/QtCreator/bin
1
2
然后执行. ~/.bashrc

3.如过编译时提示没有-lGl,则是缺少该库，通过apt install libgl1-mesa-dev即可安装。
