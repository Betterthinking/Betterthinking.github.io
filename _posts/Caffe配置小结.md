---
layout: post
title: Caffe配置小结
author: Li Yuxi
---

# 序
在博文开始之前，首先声明一下这是自己写的第一篇博文，其中不乏用词不准确或冗长多余之处，还请各位谅解，有好的建议或修改之处欢迎联系我的邮箱[lyxok1@sjtu.edu.cn](lyxok1@sjtu.edu.cn)进行指正~

好的，话不多说，进入正题。这学期由于实验室工作，需要自己在电脑上配置Caffe环境，由于自己机器配置不够，于是先是用的好心室友提供的笔记本，后来又自己买了主机，先后两次配置了Caffe环境。虽然网络上的配置教程林林总总，但机器个体差异不同导致自己不可避免地踩了不少的坑。于是决定配置完后把自己的踩坑经历总结一下，也希望后来配置环境的朋友们能够避免重蹈覆辙。

这次我主要以后来在台式机上配置Caffe的经历为主，显卡为GTX 1080，配置环境为Ubuntu14.04+CUDA8.0+cudnn8.0+OpenCV2.4.13，安装并编译了Pycaffe接口，没有编译Matlab接口。配置过程中主要参考了一下几篇博文：
* [http://blog.csdn.net/ubunfans/article/details/47724341/](http://blog.csdn.net/ubunfans/article/details/47724341/)
* [http://blog.csdn.net/fengbingchun/article/details/53844852](http://blog.csdn.net/fengbingchun/article/details/53844852)
* [http://coldmooon.github.io/2015/08/03/caffe_install/](http://coldmooon.github.io/2015/08/03/caffe_install/)

顺便把Caffe的官网配置教程贴在这里：
* [http://caffe.berkeleyvision.org/install_apt.html](http://caffe.berkeleyvision.org/install_apt.html)

# 安装基本依赖库
```shell
sudo apt-get update
sudo apt-get install build-essential 
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libboost-all-dev libhdf5-serial-dev libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler
```

# 下载并安装CUDA8.0
这里我采用的是离线.deb安装的方式，首先进入Nvidia官网[https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)下载CUDA的安装包，这里需要选择合适的操作系统和安装方式，由于我是离线.deb安装，因此选择的deb(local)一项。

这里默认所有下载文件以及压缩包都下载到了`home/username/Download`目录下，进入该目录，解压并安装：
```shell
sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb  
sudo apt-get update  
sudo apt-get install cuda
```

## 注意事项
1. 下载的CUDA包自带Nvidia驱动，有的教程推荐驱动与CUDA分开安装，但是我是直接使用的自带驱动，并没有太大问题
2. 很多教程中安装完CUDA后直接重启系统`sudo reboot`,但这里是自己遇到的第一个大坑，重启后直接卡在Ubuntu界面了，登录界面都进不去，百度谷歌也找不到解决方法，后来在知乎的一个角落里终于找到了原因以及不是办法的办法：由于我的电脑是双显卡的，当当前显卡切换为Nvidia独立显卡时，会导致以上进入不了登录界面的情况，因此在不跑程序时，或者是关机重启前，要确保当前显卡为intel集显。安装的CUDA包中有自带的显卡查询工具`prime-select`,通过指令`prime-select query`查询当前显卡，若是Nvidia，则用`sudo prime-select intel`切换回集显，再关机。如果一不小心在独显状态下关机导致又卡在Ubuntu界面或登录界面时，可以`ctrl+alt+F1`进入`tty`,在执行显卡切换并重启。
