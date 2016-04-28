---
title: Python学习（四）之函数
date: 2016-04-22 00:39:49
tags:
- Python
- 函数
categories: Python
---
![](http://7xsy4k.com2.z0.glb.qiniucdn.com/TlJDUlRVQVBVYzh2cExEZ0drcjVsakh3TWR1WTVySU1RV3ZyeGJvMzR0U3Eva0IxcGdDOE1BPT0.jpg)
# 定义一个函数
* 你可以定义一个由自己想要功能的函数，以下是简单的规则：
* 函数代码块以 def 关键词开头，后接函数标识符名称和圆括号 ()。
* 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
* 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
* 函数内容以冒号起始，并且缩进。
* return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。
**默认情况下，参数值和参数名称是按函数声明中定义的的顺序匹配起来的。**
<!--more-->

# 函数调用
定义一个函数：给了函数一个名称，指定了函数里包含的参数，和代码块结构。
这个函数的基本结构完成以后，你可以通过另一个函数调用执行，也可以直接从 Python 命令提示符执行。
```python
def test(content,n):
	"函数调用"
	print(content*n)
	return
# 函数开始调用
test("Test\n",3)
```
# 按值传递参数和按引用传递参数
在 Python 中，所有参数（变量）都是按引用传递。如果你在函数里修改了参数，那么在调用这个函数的函数里，原始的参数也被改变了。例如：
```python
def test(list1):
		"传参数"
		list1.append(3);
		print(list1)
		return

lis=[1,24,5,6]
test(lis)
print(lis)
```
但是你换成python里面自带的变量类型，比如int，他是不会变的，具体原因，看另一篇博客——Python踩过的坑


以下是调用函数时可使用的正式参数类型：

* 必需参数
* 关键字参数
* 默认参数
* 不定长参数

## 必需参数
必需参数须以正确的顺序传入函数。调用时的数量必须和声明时的一样。
调用printme()函数，你必须传入一个参数，不然会出现语法错误：
```python
#可写函数说明
def printme( str ):
   "打印任何传入的字符串"
   print (str);
   return;
#调用printme函数
printme();
```
错误如下：
```bash
Traceback (most recent call last):
  File "/Users/tangbo/Study/Code/Python/AutoStudy/test.py", line 42, in <module>
    printme();
TypeError: printme() takes exactly 1 argument (0 given)
```
## 关键字参数
关键字参数和函数调用关系紧密，函数调用使用关键字参数来确定传入的参数值。
使用关键字参数允许函数调用时参数的顺序与声明时不一致，因为 Python 解释器能够用参数名匹配参数值。列子：
```python
def speak(name, age):
    print("My name is %s, %d yeas old" % (name,age))
speak(age = 5,name='Python')
```
## 默认参数
调用函数时，如果没有传递参数，则会使用默认参数。以下实例中如果没有传入 age 参数，则使用默认值
```python
def speak(name,age=12):
    print("My name is %s, %d yeas old" % (name,age))
speak('Python')
```
**但是下面这种写法就是错的**
```python
def speak(age=12,name):
    print("My name is %s, %d yeas old" % (name,age))
speak('Python')
```
**这种也是错的**
```python
def speak(age=12,name):
    print("My name is %s, %d yeas old" % (name,age))
speak(name='Python')
```
## 不定长参数
你可能需要一个函数能处理比当初声明时更多的参数。这些参数叫做不定长参数，和上述2种参数不同，声明时不会命名。基本语法如下：
```python
def functionname([formal_args,] *var_args_tuple ):
   "函数_文档字符串"
   function_suite
   return [expression]
```
加了星号（*）的变量名会存放所有未命名的变量参数。如果在函数调用时没有指定参数，它就是一个空元组。我们也可以不向函数传递未命名的变量。如下实例：
```python
def test(first, * arg1):
	print(first)
	for x in arg1:
		print(x)
test(1,'test','python')
```
## 匿名函数
python 使用 lambda 来创建匿名函数。
所谓匿名，意即不再使用 def 语句这样标准的形式定义一个函数。

* lambda 只是一个表达式，函数体比 def 简单很多。
* lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。
* lambda 函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。
* 虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

**语法**
lambda 函数的语法只包含一个语句，如下：
```python
lambda [arg1 [,arg2,.....argn]]:expression
```
例子：
```python
sum  = lambda arg1,arg2: arg1+arg2
print(sum(1,3))
```
实在没想清楚设计这货有啥意思，过...

# return语句
return [表达式] 语句用于退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None。例子
```python
def sum(arg1,arg2):
    return arg1+arg2
print(sum(1,2))
```
# 变量作用域
Pyhton 中，程序的变量并不是在哪个位置都可以访问的，访问权限决定于这个变量是在哪里赋值的。
变量的作用域决定了在哪一部分程序可以访问哪个特定的变量名称。两种最基本的变量作用域如下：

* 全局变量
* 局部变量

全局变量和局部变量
定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域。
局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中。如下实例：
```python
total = 10
def sum(arg1,arg2):
	#计算两个参数的和#
	total = arg1+arg2
	print("函数内部的total=%s" % total)
	return total
sum(1,2)
print('函数外部的total:%s' % total)
```
# 参考
[1]. http://www.runoob.com/python3/python3-function.html

