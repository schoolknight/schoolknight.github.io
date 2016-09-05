---
layout: "post"
title: "windows环境下安装NodeJS需要的编译环境"
date: "2016-09-05 09:31"
---
Windows在日常应用中不可替代，有时却让程序员咬牙切齿，但还是要默默忍受。

我因为在日常使用的台式机上实在无法忍受Linux，又没钱买Mac，所以所有的台式机都是使用的Win10。
为了进行NodeJS的开发，我所有的机器都配置了NodeJS的环境，特别是NodeJS需要的编译环境尤其比较棘手。

## 为什么NodeJS需要编译环境？

最开始我认为NodeJS是基于JS的，只要有V8的运行环境，NodeJS的代码就是跨平台的。
这句话也对也不对，你写的NodeJS的代码确实是跨平台的，但很多我们使用到的库需要通过`node-gyp`在本地进行编译，才能进行使用，比如我目前的工作中所使用到的`xml2json`和`msgpack`。

## 有什么其他办法吗？

最简单的办法是：不要用这个库了。。。。
很多库都有替代品，比如我使用的XML转换Json的`xml2json`就可以使用`xml2js`来代替，不需要本地的编译环境。

## 开始安装

言归正传，我们开始安装NodeJS在Windows下需要的编译环境。

### 0.安装NodeJS
这里就不赘述了，直接官网下载安装包，双击安装。

### 1.安装VS编译环境
这里有两种方式，我也说不出哪种方法比较管用。

- 安装[Microsoft Build Tools 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48159)
- 安装[Visual Studio Express 2015](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx)
  - 可能需要安装额外的组件比如Win10 SDK等，可以通过VS新建一个Win32的工程，相关的组件就会安装的。

## 3.配置NPM
在工程的根目录下使用`npm install`安装需要的库，如果报错可按照下面的方法处理：

- 报错内容：` error MSB4132: 无法识别工具版本“2.0”。可用的工具版本为 "12.0", "14.0", "4.0"`类似的错误
  - 解决方法：制定MSVS版本， 使用命令 `npm install --msvs_version=2015`
- 报错内容：` error C2373: '__pfnDliNotifyHook2': redefinition;`类似的错误
  - 解决方法：更新NPM，使用命令 `npm install -g npm@next`，更新完之后再运行 `npm install --msvs_version=2015`

## 番外篇
国内许多地方直接通过`npm`安装NodeJS库无法连接（还是大学网络好，都直接可以连接），可以使用淘宝的[镜像](http://npm.taobao.org/)。
具体的设置方法里面都有，还算比较方便。
