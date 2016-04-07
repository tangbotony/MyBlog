---
title: Mac 安装 Python版本管理器——pyenv
date: 2016-04-05 22:36:49
categories: Software Installation
tags: 
- Python版本管理器
- pyenv
- Mac
- OS X
---
{% img /images/20160329/i.jpg%}
## 什么是pyenv
引用一下官方文档的第一句话：
>pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

也就是说pyenv是一种python管理器，可以同时管理多个共存的python版本，方便你在他们之间来回的切换。<!-- more -->当然如果你就只有一个python版本的话，那么这个软件对于你没有用，但是，我相信你一定会遇到这种情况：
>有一天，你忘记带自己的电脑了，当然你可能会说“笑话，作为一名程序猿，电脑怎么会离开我，机在人在”。那好吧，我换一个场景，你需要把自己的代码上传到服务器运行，但是服务器的Python版本有点低，和你本地的开发环境不一样。而你，作为一名时尚的程序猿，那是有新特性就必须要用上的啊，必须用最新版本的Python，这样才能显示出你的逼格。但是现在只有旧的运行环境，为了运行你的程序，只有两个办法，要么修改代码，要么换环境。改代码代价会有点高，还怕改出Bug，所以只有换Python的环境，装一个最新版的Python。如果你是一个不负责任的人，那么你就卸载服务器上的Python环境，换上一个新的。为什么说你不负责尼，因为现在服务器上有运行的Python程序，就需要低版本的一些特性，直接卸载，服务器就会出问题，所以你别无选择，只能安装两个版本的Python，现在你就需要这个软件了。

## 如何安装pyenv
**系统：OS X EI Capitan**
### HomeBrew 安装
如果你不知道HomeBrew的话，那就看看[http://brew.sh](http://brew.sh/)，HomeBrew是一个包管理软件，类似于Android上的豌豆荚之类的软件。基本上80%的Mac电脑都会安装这个软件，这个软件的作者是 Max Howell，关于他还有一个小故事，2015年的时候他去Google面试，但是由于不会写翻转二叉树，[被Google拒绝](http://www.pingwest.com/sorry-cant-hire-you/)，回信是这样：
>Google: 90% of our engineers use the software you wrote(HomeBrew), but you can't invert a binary tree on a whiteboard so fuck off.

我们90%的工程师都用你写的软件，但抱歉我们不能聘用你。此事在网上引起激烈的争论。例如知乎：[如何看待 Max Howell 被 Google 拒绝?](https://www.zhihu.com/question/31202353)

#### 安装命令
```bash
$ brew update
$ brew install pyenv
```
### GitHub Checkout安装
#### 安装命令
``` bash
$ git clone https://github.com/yyuu/pyenv.git ~/.pyenv
```
接下来就是添加环境变量，如果你用的是Oh My Zsh，那就用第二种方案，如果是Bash，就第一种，如果你不知道我这句话在说什么，那就是第一种添加环境变量的方式，也就是Bash。
#### 添加环境变量
第一种Bash：
``` bash
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
```

第二种 Oh My Zsh：
``` bash
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(pyenv init -)"' >> ~/.zshrc 
```
## 安装Python
``` bash
$ pyenv install --list //查看可安装的python版本
$ pyenv install 3.5.0 安装python3.5.0
```
然后就开始报错了，错误如下:
>zipimport.ZipImportError: can’t decompress data; zlib not available

{% img /images/20160405/a.png%}

缺乏zlib库，解决方案一：在终端输入xcode-select --install，然后安装命令行工具（即使你安装了xcode）
```bash
$ xcode-select --install
```
解决方案二：用HomeBrew安装zlib
```bash
$ brew install zlib
```
我是用第一种方案解决的，第二种方案是网上查的，没有机会试。安装完之后，需要重启终端。
## 查看当前已安装的python版本
``` bash
$ pyenv versions
* system (set by /Users/tangbo/.pyenv/version)
  3.5.0
```

其中的星号表示当前正在使用的是系统自带的python。

## 设置全局的python版本
```bash
$ pyenv global 3.5.0
$ pyenv versions    
  system
* 3.5.0 (set by /Users/tangbo/.pyenv/version)
```

## 参考
[1]. https://github.com/yyuu/pyenv#basic-github-checkout
