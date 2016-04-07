---
title: Markdown MathJax 的用法
date: 2016-03-29 20:11:42
tags:
- Markdown
- MathJax
categories: Markdown
---
{% img /images/20160329/e.jpg%}  
Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。它的诞生让很多笔者更加专注于写作，而不是排版问题。当然Markdown也不是非常完美的语言，它也有不擅长的东西，比如对数学公式的支持，可以说Markdown本身对数学公式是没有任何的支持能力，只能通过第三方插件来解决，其中最简单的解决方案就是MathJax了。MathJax是一款运行在浏览器中的开源的数学符号渲染引擎，使用MathJax可以方便的在浏览器中显示数学公式，不需要使用图片。目前，MathJax可以解析Latex、MathML和ASCIIMathML的标记语言。所以说安装好MathJax后，我们只需要用LaTex把公式写出来，网页就能够显示出公式了，下面我们就来看看如何安装MathJax。
<!-- more -->
## 获取MathJax
获取MathJax的方法有三种，最简单的方法就是使用分布式网络服务中的MathJax的副本，它位于 cdn.mathjax.org，但是你也可以下载并安装一个MathJax的副本到你的服务器，或者使用在你本地硬盘的副本（这样是不需要使用网络）。这里我们采用的是最简单的方法，采用CDN，只需要在你书写的.md文件的第一行加上如下的js代码：
``` JavaScript
<script type="text/javascript" async
  src="//cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```
上面的js引入的MathJax默认的定界符是\$\$...\$\$和\\ [...\\]，行内定界符是\\ (...\\ )，官方文档还给出了另一种方案：
``` javascript
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]}
});
</script>
<script type="text/javascript" async src="path-to-mathjax/MathJax.js?config=TeX-AMS_CHTML"></script>
```
通过这种方式引入的MathJax，包含在段落之中的公式就可以通过\$...\$来作为定界符，比较简单，但是会有一个问题，官方文档是这么描述的：
>The default math delimiters are \$\$...\$\$ and \\ [...\\ ] for displayed mathematics, and \\ (...\\ ) for in-line mathematics. Note in particular that the \$...\$ in-line delimiters are not used by default. That is because dollar signs appear too often in non-mathematical settings, which could cause some text to be treated as mathematics unexpectedly. For example, with single-dollar delimiters, ”... the cost is \$2.50 for the first one, and \$2.00 for each additional one ...” would cause the phrase “2.50 for the first one, and” to be treated as mathematics since it falls between dollar signs.

这种方式引入的MathJax在$符号上会有冲突，所以大家根据自己的情况来选择哪一种方式映入MathJax。另外引入MathJax的两种方案大家可以参考[MathJax的中文帮助文档](http://mathjax-chinese-doc.readthedocs.org/en/latest/start.html)。

## MathJax的用法
LaTeX的数学公式有两种：行内公式和块级公式。行内公式放在文中与其它文字混编，块级公式单独成行。都使用美元符号进行标记显示。
### 行内公式
**使用方法：** 使用一个美元符号包围起来（这里我们是第二种引入MathJax的方式）。
**列子：** $\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$
```
$sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$
```
### 块级公式
**标记方法：**使用两个美元符号包围起来
**例子：**$$ x = \dfrac{-b \pm \sqrt{b^2 - 4ac}}{2a}.$$
```
$$ x = dfrac{-b pm sqrt{b^2 - 4ac}}{2a}.$$
```
一个完整的列子，当我们在Markdown里面这么写时：
``` bash
When $a \ne 0$, there are two solutions to \\(ax^2 + bx + c = 0\\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
```
在网页上显示的效果如下：
When $a \ne 0$, there are two solutions to \\(ax^2 + bx + c = 0\\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

至于公式的LaTeX形式，不知道的可以查[MathJax basic tutorial and quick reference](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)，如果感觉英文看起来比较麻烦，比如像我，那么可以参照Ryan Zhao写的[Mathjax与LaTex公式简介](http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/)来看，这里就不重复的造轮子了。
## 参考
[1]. http://docs.mathjax.org/en/latest/start.html
[2]. http://meta.math.stackexchange.com/questions/5020/

















