#### 主要记录了将Pyhon工程环境移植到没有网络的内网环境

1. 首先下载python、 pycharm安装包，对python、pycharm进行解压安装。
2. 遇到的第一个问题是安装python报错，无法安装pip。 解决办法：通过另一台电脑网上下载zlib包解决这个问题。
3. 遇到的第二问题是安装部分包时会报错，" no module named "_ctypes" "， 解决办法：下载libffi包，我用的是ubantu系统，搜索libffi-dev，如果遇到安装其他的问题，可能需要一些其他的包。
4. 将python安装好之后，在原始的环境中可以通过，pip3 freeze > requirements.txt 生成所有所需要的依赖包。
5. 然后可以通过pip3 download -r requirements.txt -d 路径   可以直接将所有的包放在设置的路径下面。部分包如果不能自动下载，可以通过网上自己下载。
6. pip3 install --no-index --find-links=路径 -r requirements.txt 可以直接搞定安装环境。
7. 在运行代码时，报错显示缺少_bz2包，这个包也是python的底层依赖包，网上下载后，安装即可。
8. 注意：下载安装的libffi 和 _bz2包 最好都是tar.gz格式的，我原始下载的.rpm和.deb经过一番疯狂操作后，都没有安装成功。而且底层包安装后要重新编译安装python
9. 注意：安装过程中遇到的问题，ubantu系统突然显示no spcae on device （我不知道是不是因为我的原因，python安装了好几遍），内存满的原因是因为ubantu系统下log日志中 ./cups文件大量生成，具体的解决方法是大佬搞定的，步骤我并不太清楚。再次记录一下。