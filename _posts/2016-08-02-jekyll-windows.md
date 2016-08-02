---
layout: post
title: Windows上配置jekyll
categories: [tool]
tags: [jekyll]
---
尝试在公司的Win7系统上安装jekyll，踩到许多坑，在这里记录一下

## 1.基本安装流程
基本的安装流程可以参考[这篇文章](http://jingyan.baidu.com/article/3c343ff7e5c0980d377963d9.html)，需要注意的是安装jekyll时，不要使用默认的`gem install jekyll`，默认安装的jekyll 3.2.0存在Windows的兼容性错误，最好使用`gem install jekyll -v 3.1.6`

## 2.错误解决方法

### cannot load such file -- XXXXX
缺少某个gem包，使用命令`gem install XXXXX`来解决。

中间存在某些特殊情况：
- 如果提示缺少pygments相关的包，需要通过python安装，具体的方法可以通过[这篇文章](http://jingyan.baidu.com/article/925f8cb8f6422ac0dde056ee.html)查找。
- 如果提示缺少jekyll-paginate，并且安装后无效，修改`Gemfile`，加入
{% highlight shell %}
gem 'jekyll'
gem "jekyll-paginate"
{% endhighlight %}
之后运行`bundle install`，运行服务器使用`bundle exec jekyll serve`

###  Could not find jekyll-3.2.0 in any of the sources
由于bundler对于版本的限制导致，修改`Gemfile.lock`文件，修改成`jekyll (3.1.6)`
