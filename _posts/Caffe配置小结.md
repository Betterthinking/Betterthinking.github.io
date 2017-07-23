---
layout: post
title: Caffe配置小结
author: Li Yuxi
---

# 序
在博文开始之前，首先声明一下这是自己写的第一篇博文，其中不乏用词不准确或冗长多余之处，还请各位谅解，有好的建议或修改之处欢迎联系[我的邮箱](lyxok1@sjtu.edu.cn)进行指正~

好的，话不多说，进入正题。这学期由于实验室工作，需要自己在电脑上配置Caffe环境，由于自己机器配置不够，于是先是用的好心室友提供的笔记本，后来又自己买了主机，先后两次配置了Caffe环境。虽然网络上的配置教程林林总总，但机器个体差异不同导致自己不可避免地踩了不少的坑。于是决定配置完后把自己的踩坑经历总结一下，也希望后来配置环境的朋友们能够避免重蹈覆辙。

这次我主要以后来在台式机上配置Caffe的经历为主，显卡为GTX 1080，配置环境为Ubuntu14.04+CUDA 8.0+cudnn8.0+OpenCV2.4.13，安装并编译了Pycaffe接口，没有编译Matlab接口。配置过程中主要参考了一下几篇博文：
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

#下载并安装CUDA8.0
