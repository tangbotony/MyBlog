---
title: Hexo进程守护神——Forever
date: 2016-04-07 15:06:55
categories: Hexo
tags:
- Hexo
- Forever
---
{% img /images/mac.jpg%}
## 背景
安装上Hexo也有一段时间了，但是Hexo的服务总是两三天就莫名奇妙的会停止运行，这就导致我得不断去重启，非常的麻烦，但是由于最近事情有点多，就没弄。哎，说白了，就是懒...正好今天有点空（上公选课，懒得听），就查了一下原因，打开日志看了看是因为Hexo URLDecoder这个方法出异常，导致Hexo服务就退出了，网站就无法访问。
解决方案：在这种情况下，就需要有一个进程来守护Hexo的服务进程，当Hexo的服务退出以后，守护进程那就再启动一下Hexo的服务进程，这样就能保证Hexo的服务永远在运行了，我以为Hexo 3.0 把服务器独立成了个别模块，它会解决这个问题，不幸的是我们还得自己解决。

## Forever是什么
引用一下[官网](https://github.com/foreverjs/forever)的解释:
> A simple CLI tool for ensuring that a given script runs continuously (i.e. forever).

就是说Forever可以看做是一个nodejs的守护进程，能够启动，停止，重启我们的app应用，本质上就是在forever进程之下，创建一个node app的子进程。
<!-- more -->
## Forever安装
我觉得能遇到这个问题的时候，你的Hexo Server模块都已经安装了，如果你还没有，那就看这[Hexo Server](https://hexo.io/docs/server.html)。
Forever全局安装命令:
``` bash
npm install -g forever
```
检查你的Forever是否安装成功：
```bash
forever --help
```
如果出现下面这些结果，那就安装成功了。
``` bash
 usage: forever [action] [options] SCRIPT [script-options]

  Monitors the script specified in the current process or as a daemon

  actions:
    start               Start SCRIPT as a daemon
    ...
```
## Forever让Hexo永久运行
安装完成后，需要在你的hexo根目录（与Hexo的_config.yml同一级目录）下新建一个js文件，比如app.js，向里面写入如下内容：

```JavaScript
var spawn = require('child_process').spawn;
free = spawn('hexo', ['server', '-p 4000']);

free.stdout.on('data', function (data) {
console.log('standard output:\n' + data);
});

free.stderr.on('data', function (data) { 
console.log('standard error output:\n' + data);
});

free.on('exit', function (code, signal) {
console.log('child process eixt ,exit:' + code);
});
```
当然第二行换成你需要启动的端口，现在是4000。保存退出后，就需要启动这个运用，命令如下：
```bash
forever --minUptime 10000 --spinSleepTime 26000 start app.js
```
至于--minUptime和--spinSleepTime这两个参数的解释大家可以看[参考的第二个链接](http://blog.pillakloud.com/blog/2015/06/23/node-js-%E4%B8%ADforever%E5%8F%83%E6%95%B8%E8%A7%A3%E9%87%8B-minuptime-spinsleeptime/)。查看一下是否启动成功，命令：
```bash
forever list
```
如果出现一下结果，就代表启动成功。
```bash
info:    Forever processes running
data:        uid  command                                  script forever pid  id logfile                 uptime      
data:    [0] wLz0 /root/.nvm/versions/node/v4.4.0/bin/node app.js 1226    1231    /root/.forever/wLz0.log 0:0:0:6.631 
```
如果你想停止这个服务，就用下面这个命令：
```bash
forever stop app.js
```
然后再用forever list查看已经启动的进程，看看你需要停止的进程是否已经停止。至于Forever的其它命令，你可以采用forever -h来查询。
## 参考
[1]. https://github.com/foreverjs/forever
[2]. http://blog.pillakloud.com/blog/2015/06/23/node-js
