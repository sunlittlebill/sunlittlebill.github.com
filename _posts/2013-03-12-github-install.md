---
layout: post
title: "github-install"
description: "学习GitHub"
category: hello-github
tags: [github]
---
{% include JB/setup %}

里程碑式的一天,现在介绍一下我安装github与配置 ***windows7*** +  ***GitHub Blog*** 环境。

## 注册并登录GitHub

登陆[github](https://github.com/)

## 安装 Jekyll Blog

打开[Jekyll Blog](http://jekyllbootstrap.com/)讲的很详细，下面只是简单介绍。

### 1 、**安装 Jekyll Blog**

去[github](https://github.com) 创建一个新库地址是 `你的名字.github.com`

提示，`你的名字`是GitHub username
 
### 2 、**安装 Jekyll-Bootstrap**

打开Git Shell

`git clone https://github.com/plusjade/jekyll-bootstrap.git 你的名字.github.com`

`cd 你的名字.github.com`

`git remote set-url origin git@github.com:你的名字/你的名字.github.com.git`

`git push origin master`

### 3 、**等待GitHup发布完成**

这可以需要几分钟时间，请耐心等待，等待发布成功后，就可以访问`你的名字.github.com`

### 4 、**配置Jekyll-Bootstrap环境**

安装Jekyll-Bootstrap需要Ruby环境(ruby + devkit)支持，我这里安装的版本是：

 * rubyinstaller-1.9.3-p392.exe [下载地址](http://rubyforge.org/frs/download.php/76798/rubyinstaller-1.9.3-p392.exe)

 * devkit-tdm-32-4.5.2-20111229-1559-sfx.exe [下载地址](https://github.com/downloads/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe)

安装rubyinstaller-1.9.3-p392.exe很简单，一直下一步就行；

安装devkit-tdm-32-4.5.2-20111229-1559-sfx.exe略微麻烦点，打开自解压缩包，需要配置好系统环境变量；

### 5 、**一切准备就绪，开始安装运行Jekyll**

运行 `gem install jekyll` 等待安装完成；

如果一切顺利的话，就可以启动本地Jekll环境了；

`cd 你名字.github.com `

`jekyll --server`

如果没有任何报错，那么就说明，你的环境已经搭建好了。 :)

### 6 、**增加代码高亮，安装Pygmentize**

在安装完ruby后，实际上pygmentize就已经有，但是还没有安装，需要手工安装一下，

进入到 `c:\Ruby193\lib\ruby\gems\1.9.1\gems\pygments.rb-0.3.7\vendor\pygments-main\`

提示，安装Pygmentize需要python支持，如果没有安装，请首先安装python，根据Windows x86或者x64选择不同的安装文件，这跟不已经安装最新版，跟ruby一样，安装稳定版就好，[下载地址](http://www.activestate.com/activepython/downloads)，我本机安装的是`ActivePython-2.7.2.5-win64-x64.msi`[下载地址](http://www.activestate.com/activepython/downloads/thank-you?dl=http://downloads.activestate.com/ActivePython/releases/2.7.2.5/ActivePython-2.7.2.5-win64-x64.msi)，直接安装点下一步就行。

 * `python setup.py install`

 * `pygmentize -S default -f html > pygments.css` 生成样式

 	拷贝 pygments.css 至 assets/themes/twitter/css

	修改 _includes/themes/twitter/default.html

 * 添加 `<link href="/assets/themes/css/pygments.css" rel="stylesheet" type="text/css" media="all">`


### 7 、**本地测试运行**

发现文件中有中文，jekyll报错了；(报错重要信息)

`YAML Exception reading index.md: invalid byte sequence in GB2312'

`Liquid Exception: invalid byte sequence in GB2312 in index.md`

解决方法：
定位到`C:\Ruby193\lib\ruby\gems\1.9.1\gems\jekyll-0.11.2\lib\jekyll\convertible.rb`(默认ruby安装目录)下面28行。

找到 `self.content = File.read(File.join(base, name))`

替换成 `self.content = File.read(File.join(base, name), :encoding => "utf-8")`

再重新启动jekyll，问题解决了。


### 8 、**测试并发布**

ruby
{% highlight ruby%}
def hello
	puts "hello"
end
{% endhighlight %}

python
{% highlight python%}
def hello
	print "hello"
{% endhighlight %}

java
{% highlight java%}
public static void main(String[] args) {
	System.out.println("Hello World");
}
{% endhighlight %}

javascript
{% highlight javascript%}
document.getElementById("helloworld");
{% endhighlight %}