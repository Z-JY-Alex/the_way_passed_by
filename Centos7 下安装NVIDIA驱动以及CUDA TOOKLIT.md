### Centos7 下安装NVIDIA驱动以及CUDA TOOKLIT

#### 安装NVIDIA驱动

#####  1、查看基本信息

#uname -vr![image-20211012101746294](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012101746294.png)

2、查看硬件信息

#lspci | grep -i nvidia

![image-20211012101727262](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012101727262.png)

看不出来显卡型号的可以Google一下。

##### 3、现在是没有安装GPU驱动的，也无法用nvidia命令查看

#nvidia-smi

-bash: nvidia-smi: command not found

##### 4、使用yum安装gcc

#yum -y install gcc gcc-c++ kernel-devel

##### 5、ELRepo源安装

ELRepo源提供了nvidia-detect命令，会自动寻找合适的驱动，然后根据显示的结果，用yum就能完成安装

\# 导入公钥(公共密钥)
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
\# 为RHEL-7、SL-7/CentOS-7安装elrepo
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm

##### 6、查找合适驱动

\# 安装显卡检查程序

#yum install nvidia-detect  

\# 查找合适的显卡驱动

#nvidia-detect

![image-20211012101607159](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012101607159.png)

##### 7、安装驱动

\# 根据查询结果，安装合适版本驱动

#yum -y install kmod-nvidia

##### 8、重启

#reboot
重启之后，使用#nvidia-smi指令即可查看。

![image-20211012101941144](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012101941144.png)





#### ————————————————————————————————————————————————

驱动安装成功后，发现#nvcc -V指令不能用，无法查看到cuda的版本，且#cd /usr/local/ 目录下没有cuda

#### 安装CUDA Tooklit

##### 1、登录cuda tooklit官网下载页面

https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=CentOS&target_version=7&target_type=runfile_local（也可以百度）

![image-20211012102738035](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012102738035.png)

建议选择.run文件。（我在rpm安装过程中报错，显示安装包冲突）

#### 2、按步骤执行命令

选择完合适的系统的安装方式后，下面会跳出安装步骤命令。

###### 注意：安装过程冲取消Driver安装，不然会和之前安装的驱动冲突

![image-20211012103052944](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012103052944.png)

##### 3、安装完成后配置环境变量

将中间两行贴进去就行

#vim /etc/profile

export PATH=/usr/local/cuda/bin:$PATH

export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

#source /etc/profile

#### 结果

#nvcc -V

![image-20211012103502756](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012103502756.png)



————————————————————————————————————————————————————————————



### NVIDIA-Docker 安装

链接：[Installation Guide — NVIDIA Cloud Native Technologies documentation](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#installing-on-centos-7-8)

直接按照教程走就可以。

也可以先按照Docker的官方文档：[Install Docker Engine on CentOS | Docker Documentation](https://docs.docker.com/engine/install/centos/)

先安装docker在安装NVIDIA-Docker。

