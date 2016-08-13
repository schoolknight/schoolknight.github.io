---
layout: "post"
title: "安装 caffe-segnet"
date: "2016-08-13 20:06"
---

最近接的私活是配置一个关于街景图片的神经网络学习框架**[Segnet](http://mi.eng.cam.ac.uk/projects/segnet/)**，在我看来并不是十分靠谱，尝试投CVPR'15，但是悲剧了，但开源程度还是不错，Github页面和自己的tutorial页面都做的不错。**Segnet**使用了一个开源的图像神经网络框架**[Caffe](http://caffe.berkeleyvision.org/)**。下面简单介绍配置**Caffe**的Python+CPU版本在Ubuntu 14.04上的配置方法。

## 1 安装依赖
**Caffe**需要许多依赖包，下面简单介绍各个依赖包。

### 1.1 基本依赖
```
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```

### 1.2 ATLAS或BLAS
安装ATLAS(Automatically Tuned Linear Algebra Software)，提供主要的矩阵计算的库：
```
sudo apt-get install libatlas-base-dev
```
如果追求更快的计算速度，可以使用OpenBLAS或MKL

### 1.3 python
需要安装Python的编译支持包
```
sudo apt-get install python-dev
```
### 1.4 OpenCV2
因为Python程序需要，推荐版本2.4.9版本，需要编译安装，推荐[教程](http://my.oschina.net/u/1757926/blog/293976)。

### 1.4 CUDA
因为我们使用CPU版本，不需要GPU计算，所以可以跳过。

## 2 编译
首先从[Caffe-Segnet](https://github.com/alexgkendall/caffe-segnet)获得Segnet的源码：
```
git clone git@github.com:alexgkendall/caffe-segnet.git
```
到目录下，建立Makefile，并修改细节：
```
cp Makefile.config.example Makefile.config
vim Makefile.config
```
需要修改的内容如下：

- 改成仅使用CPU运算 `CPU_ONLY := 1`
- 使用ATLAS `BLAS:=atlas`
- 根据Python安装路径修改相应的部分

编译Python版本
```
make pycaffe
```

## 3 获得样例程序和训练好的模型
相应的模型可以从[Segnet-Tutorial](https://github.com/alexgkendall/SegNet-Tutorial)中获得，权值文件的体积比较大，需要单独下载。
但是样例的Webdemo程序需要相应的修改，什么时候心情好了把自己的程序放出来。
