---
title: Python学习（三）之流程控制和迭代器与生成器
date: 2016-04-21 00:31:27
tags:
- 流程控制
- 迭代器
- 生成器
categories: Python
---
![](http://7xsy4k.com2.z0.glb.qiniucdn.com/OVg2eEM2UlA1THhrYzVEZm8wb3pqd1daczdwQXR2ZmZDUEhYNlluTnJIOHp0Rk02M08xMm5nPT0.jpg)
# Python3 条件控制
## if 语句
```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```
* 如果 "condition_1" 为 True 将执行 "statement_block_1" 块语句
* 如果 "condition_1" 为False，将判断 "condition_2"
* 如果"condition_2" 为 True 将执行 "statement_block_2" 块语句
* 如果 "condition_2" 为False，将执行"statement_block_3"块语句
* Python 中用 elif 代替了 else if，所以if语句的关键字为：if – elif – else。
<!--more-->
注意：
1、每个条件后面要使用冒号（:），表示接下来是满足条件后要执行的语句块。
2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。
3、在Python中没有switch – case语句。
列子：
```python
while True:
    age = int(input("请输入你家狗狗的年龄: "))
    print("")
    if age < 0:
        print("你是在逗我吧!")
    elif age == 1:
        print("相当于 14 岁的人。")
    elif age == 2:
        print("相当于 22 岁的人。")
    elif age > 2:
        human = 22 + (age - 2) * 5
        print("对应人类年龄: ", human)
```

# Python3 循环语句
## while 循环
Python中while语句的一般形式：
```python
while 判断条件：
    语句
```
列子：

```python
a = 1
sum = 0
dis = 100
while a <= dis:
    sum += a
    a = a + 1
print('从 1 加到 %d = %d' % (dis, sum))
```
**while 循环使用 else 语句**
在 while … else 在条件语句为 false 时执行 else 的语句块：
```python
a = 1
sum = 0
dis = 100
while a <= dis:
    sum += a
    a = a + 1
else:
    print('循环结束时a=%d'% a)
print('从 1 加到 %d = %d' % (dis, sum))
```
# for 语句
Python for循环可以遍历任何序列的项目，如一个列表或者一个字符串。
for循环的一般格式如下：
```python
for <variable> in <sequence>:
    <statements>
else:
    <statements>
```
列子：
```python
list1 = ['C', 'Java', 'Python']
for x in list1:
    print(x)
```
break 跳出循环
```python
list1 = ['C', 'Java', 'Python', 'C++']
for x in list1:
    if x == 'Python':
        print('学习')
        break
    else:
        print("%s 太难，不学" % x)
```
## range()函数
如果你需要遍历数字序列，可以使用内置range()函数。它会生成数列，例如:
```python
list1 = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
for i in range(len(list1)):
    print(list1[i])
```
也可以使range以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长'):
```python
for i in range(1,10,3):
    print(i)
```
## break和continue语句及循环中的else子句
break 语句可以跳出 for 和 while 的循环体。如果你从 for 或 while 循环中终止，任何对应的循环 else 块将不执行。 实例如下：
```python
for n in range(2, 10):
    for x in range(2, n):
        if(n % x == 0):
            print(n, '等于', x, '*', n // x)
            break
    else:
        print(n, ' 是质数')
```
## pass 语句
Python pass是空语句，是为了保持程序结构的完整性。
pass 不做任何事情，一般用做占位语句，如下实例
```python
 while True:
...     pass  # 等待键盘中断 (Ctrl+C)
```
# Python3 迭代器与生成器
## 迭代器
迭代是Python最强大的功能之一，是访问集合元素的一种方式。。
迭代器是一个可以记住遍历的位置的对象。
迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。
迭代器有两个基本的方法：iter() 和 next()。
字符串，列表或元组对象都可用于创建迭代器：
```python
list1 = ['a', 1, 'b']
it = iter(list1)
for c in it:
    print(c)
```
for循环迭代
```python
list1 = ['a', 1, 'b']
it = iter(list1)
while True:
    try:
        print(next(it))
    except StopIteration:
        SystemExit
```
## 生成器
在 Python 中，使用了 yield 的函数被称为生成器（generator）。
跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。
在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回yield的值。并在下一次执行 next()方法时从当前位置继续运行。
以下实例使用 yield 实现斐波那契数列：
```python
import sys
def fib(n):
    a,b,count = 0,1,0
    while True:
	if count>n:
	    return
	yield a
	a,b = b,a+b
	count+=1
it = fib(10)
while True:
    try:
	print(next(it))
    except Exception:
	sys.exit()
```
**我觉得可以这么理解，返回的是一个变量的指针，然后这个指针指向的地址块里面按顺序存放了这个变量的历史数据。**这个说法虽然不对，但是对于理解非常的适合我。
# 参考
[1]. http://www.runoob.com/python3
