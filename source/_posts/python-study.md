---
title: Python学习（一）之基础语法
date: 2016-04-17 01:02:47
tags:
- Python
- 入门
categories: Python
---
![](http://7xsy4k.com2.z0.glb.clouddn.com/c.jpg)
看机器学习教程到现在，发现很多算法库都是用Python实现的，感觉Python是必须要会的了，虽然之前零零散散学过点，但是都不系统，所以今天就系统来学习Python。以下教程适合有点编程经验的人看，主要基本上是语法规则，如果有编程经验，基本上看完一遍，就可以上路了。
## Python安装
网上教程很多，自行Google。
## Python基本语法
### 查看Python版本
``` bash
python -V
```
或者进入交互式环境查看，python
```bash
➜  ~  python
Python 3.5.0 (default, Apr  5 2016, 21:49:02) 
[GCC 4.2.1 Compatible Apple LLVM 7.3.0 (clang-703.0.29)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
```
### 编码
默认情况下，Python 3 源码文件以 UTF-8 编码，所有字符串都是 unicode 字符串。 当然你也可以为源码文件指定不同的编码：
```python
# -*- coding: cp-1252 -*-
```
### 标识符
* 第一个字符必须是字母表中字母或下划线'_'
* 标识符的其他的部分有字母、数字和下划线组成
* 标识符对大小写敏感

在Python 3中，非-ASCII 标识符也是允许的了。

### python保留字
保留字即关键字，我们不能把它们用作任何标识符名称。Python的标准库提供了一个keyword module，可以输出当前版本的所有关键字：
```python
import keyword
keyword.kwlist
```
<!--more-->
### 注释
Python中单行注释以 # 开头，实例如下：
```python
#!/usr/bin/python3
# 第一个注释
print("Hello, Python!") # 第二个注释
```

### 行与缩进
python最具特色的就是使用缩进来表示代码块，不需要使用大括号({})。
缩进的空格数是可变的，但是同一个代码块的语句必须包含相同的缩进空格数。实例如下：
```python
if True:
	print ("True")
else:
	print ("False")
```
缩进数的空格数不一致，会导致运行错误：
```python
# coding: utf-8
if True:
    print ("Answer")
    print ("True")
else:
    print ("Answer")
  print ("False")    # 缩进不一致，会导致运行错误
```
错误如下：
```python
File "/Users/tangbo/Study/Code/Python/AutoStudy/test.py", line 7
    print ("False")    # 缩进不一致，会导致运行错误
                                                               ^
IndentationError: unindent does not match any outer indentation level
[Finished in 0.0s with exit code 1]
[shell_cmd: python -u "/Users/tangbo/Study/Code/Python/AutoStudy/test.py"]
[dir: /Users/tangbo/Study/Code/Python/AutoStudy]
[path: /usr/bin:/bin:/usr/sbin:/sbin]
```
### 多行语句
Python 通常是一行写完一条语句，但如果语句很长，我们可以使用反斜杠(\)来实现多行语句，例如：
```python
one = "one"
two = "two"
three = "three"
total = one + \
    two + \
    three
print(total)
```
在 [], {}, 或 () 中的多行语句，不需要使用反斜杠(\)，例如：
```python
total = ['one', 'two',
         'three']
print(total)
```
### 数据类型
python中数有四种类型：整数、长整数、浮点数和复数。

* 整数， 如 1
* 长整数 是比较大的整数
* 浮点数 如 1.23、3E-2
* 复数 如 1 + 2j、 1.1 + 2.2j

### 字符串
* python中单引号和双引号使用完全相同。
* 使用三引号('''或""")可以指定一个多行字符串。
* 转义符 '\'
* 自然字符串， 通过在字符串前加r或R。 如 r"this is a line with \n" 则\n会显示，并不是换行。
* python允许处理unicode字符串，加前缀u或U， 如 u"this is an unicode string"。
* 字符串是不可变的。
* 按字面意义级联字符串，如"this " "is " "string"会被自动转换为this is string。

```python
# coding: utf-8
word1 = '字符串1'
word2 = "字符串2"
word3 = """这是特殊的字符串
这是特殊的字符串
这是特殊的字符串
这是特殊的字符串3
"""
word4 = r"hello \n word"
word5 = u"this is an unicode string"
word6 = "this""is""string"
print(word1)
print(word2)
print(word3)
print(word4)
print(word5)
print(word6)
```
结果：
```bash
字符串1
字符串2
这是特殊的字符串
这是特殊的字符串
这是特殊的字符串
这是特殊的字符串3

hello \n word
this is an unicode string
thisisstring
[Finished in 0.0s]
```
### 空行
函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。类和函数入口之间也用一行空行分隔，以突出函数入口的开始。
**空行与代码缩进不同，空行并不是Python语法的一部分**。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。
**记住：空行也是程序代码的一部分。**
### 等待用户输入
执行下面的程序在按回车键后就会等待用户输入：
```python
temp = input("请输入：")
print(temp)
```
### 同一行显示多条语句
Python可以在同一行中使用多条语句，语句之间使用分号(;)分割，以下是一个简单的实例：
```python
a=1;b=3;print(a+b)
```
## Python3 基本数据类型
Python 中的变量不需要声明。每个变量在使用前都必须赋值，变量赋值以后该变量才会被创建。
在 Python 中，变量就是变量，它没有类型，我们所说的"类型"是变量所指的内存中对象的类型。
等号（=）用来给变量赋值。
等号（=）运算符左边是一个变量名,等号（=）运算符右边是存储在变量中的值。例如：
```python
counter = 100          # 整型变量
miles   = 1000.0       # 浮点型变量
name    = "runoob"     # 字符串
print (counter)
print (miles)
print (name)
```
### 多个变量赋值
Python允许你同时为多个变量赋值。例如：
```python
a=b=c="Hello"
print(a)
print(b)
print(c)
```
以上实例，创建一个字符串对象，值为"Hello"，三个变量被分配到相同的内存空间上。
您也可以为多个对象指定多个变量。例如：
```python
a,b,c = 1,10.0,"Hello"
print(a)
print(b)
print(c)
```
Result:
```python
1
10.0
Hello
```
### 标准数据类型
Python3 中有六个标准的数据类型：

* Number（数字）
* String（字符串）
* List（列表）
* Tuple（元组）
* Sets（集合）
* Dictionary（字典）

#### Number（数字）
Python3 支持 int、float、bool、complex（复数）。
在Python 3里，只有一种整数类型 int，表示为长整型，没有 python2 中的 Long。
像大多数语言一样，数值类型的赋值和计算都是很直观的。
内置的type()函数可以用来查询变量所指的对象类型。
```python
a, b, c, d, e = 1, 10.0, "Hello", True, 4 + 3j
print(type(a), type(b), type(c), type(d), type(e))
```
Result:
```bash
(<type 'int'>, <type 'float'>, <type 'str'>, <type 'bool'>, <type 'complex'>)
```
#### String（字符串）
Python中的字符串用单引号('')或双引号("")括起来，同时使用反斜杠(\)转义特殊字符。
字符串的截取的语法格式如下：
变量[头下标:尾下标]
索引值以 0 为开始值，-1 为从末尾的开始位置。
加号 (+) 是字符串的连接符， 星号 (*) 表示复制当前字符串，紧跟的数字为复制的次数。实例如下：
```python
str = "python"
print(str[1:])
print(str * 4)
```
Python 使用反斜杠(\)转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 r，表示原始字符串：
```python
print("py\nthon")
print(r"py\nthon")
```
另外，反斜杠(\)可以作为续行符，表示下一行是上一行的延续。也可以使用 """...""" 或者 '''...''' 跨越多行。
注意，Python 没有单独的字符类型，一个字符就是长度为1的字符串。
与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如word[0] = 'm'会导致错误。
注意：

* 反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
* 字符串可以用+运算符连接在一起，用*运算符重复。
* Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
* Python中的字符串不能改变。

#### List（列表）
List（列表） 是 Python 中使用最频繁的数据类型。
列表可以完成大多数集合类的数据结构实现。列表中元素的类型可以不相同，它支持数字，字符串甚至可以包含列表（所谓嵌套）。
列表是写在方括号([])之间、用逗号分隔开的元素列表。
和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。
列表截取的语法格式如下：
变量[头下标:尾下标]
索引值以 0 为开始值，-1 为从末尾的开始位置。
加号（+）是列表连接运算符，星号（*）是重复操作。如下实例：
```python
list1 = [1, 1.0, "Hello", 1 + 4j]
list2 = [4 + 7j, "Hello", 1.0, 1]
print(list1[1])
print(list1[2:])
print(list1 + list2)
list1 = []
list1.append(5)
print(list1)
list1[0] = 7
print(list1)
```
Result
```bash
1.0
['Hello', (1+4j)]
[1, 1.0, 'Hello', (1+4j), (4+7j), 'Hello', 1.0, 1]
[5]
[7]
```
List内置了有很多方法，例如append()、pop()等等，这在后面会讲到。
注意：

* List写在方括号之间，元素用逗号隔开。
* 和字符串一样，list可以被索引和切片。
* List可以使用+操作符进行拼接。
* List中的元素是可以改变的。

#### Tuple（元组）
元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号(())里，元素之间用逗号隔开。
元组中的元素类型也可以不相同。
```python
tuple1 = (1, 1.0, "Hello", 1 + 4j)
tupke2 = (4 + 7j, "Hello", 1.0, 1)
print(tuple1[1])
print(tuple1[2:])
print(tuple1 + tupke2)
```
当我们视图改变里面的元素时，就会包如下的错误:
```python
# coding: utf-8
tuple1 = (1, 1.0, "Hello", 1 + 4j)
tupke2 = (4 + 7j, "Hello", 1.0, 1)
print(tuple1[1])
print(tuple1[2:])
print(tuple1 + tupke2)
tuple1[0] = 9

Result:
1.0
('Hello', (1+4j))
(1, 1.0, 'Hello', (1+4j), (4+7j), 'Hello', 1.0, 1)
Traceback (most recent call last):
  File "/Users/tangbo/Study/Code/Python/AutoStudy/test.py", line 7, in <module>
    tuple1[0] = 9
TypeError: 'tuple' object does not support item assignment
```
通过上面的错误也可以得出python是解释型语言的结论，中间报错了，不要紧，继续执行。
**虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。**
#### 集合（set）
集合（set）是一个无序不重复元素的序列。
基本功能是进行成员关系测试和删除重复元素。
可以使用大括号({})或者 set()函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。
```python
student = {'tom', 'Jim', 'jack'}
student1 = {'tom', 'Jim', 'jack', 'a'}
print(student)
print(student - student1)
a = set('abracadabra')
b = set('alacazam')
print(a)
print(b)
```
Result:
```bash
set(['Jim', 'jack', 'tom'])
set([])
set(['a', 'r', 'b', 'c', 'd'])
set(['a', 'c', 'z', 'm', 'l'])
[Finished in 0.0s]
```
#### Dictionary（字典）
字典（dictionary）是Python中另一个非常有用的内置数据类型。
列表是有序的对象结合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
字典是一种映射类型，字典用"{ }"标识，它是一个无序的键(key) : 值(value)对集合。
键(key)必须使用不可变类型。
在同一个字典中，键(key)必须是唯一的。感觉和java里面的Map对象很像啊。。。
```python
dict = {}
dict['one'] = 1
dict[2] = "Hello"
print(dict['one'])
print(dict[2])
```

另外，字典类型也有一些内置的函数，例如clear()、keys()、values()等。
注意：

* 字典是一种映射类型，它的元素是键值对。
* 字典的关键字必须为不可变类型，且不能重复。
* 创建空字典使用 { }。

```python
dict = {}
dict['one'] = 1
dict[2] = "Hello"
print(dict.keys())
print(dict.values())
```
Result:
```bash
[2, 'one']
['Hello', 1]
```
### Python数据类型转换
有时候，我们需要对数据内置的类型进行转换，数据类型的转换，你只需要将数据类型作为函数名即可。
以下几个内置的函数可以执行数据类型之间的转换。这些函数返回一个新的对象，表示转换的值。
```python
a = 1
b = 1.0
c = "Hello"
d = 1 + 7j
print(float(b))
print(hex(a))
```
## Python3 注释
确保对模块, 函数, 方法和行内注释使用正确的风格
Python中的注释有单行注释和多行注释。Python中单行注释以#开头，多行注释用三个单引号（'''）或者三个双引号（"""）将注释括起来例如：
```python
# 单行注释
'''
多行注释
多行注释
多行注释
'''

"""
多行注释
多行注释
多行注释
"""
```

## Python3 运算符
Python语言支持以下类型的运算符:

* 算术运算符
* 比较（关系）运算符
* 赋值运算符
* 逻辑运算符
* 位运算符
* 成员运算符
* 身份运算符
* 运算符优先级

### 算术运算符
以下假设变量a为10，变量b为21：

|运算符|描述                       |实例                             |
|---|-------------------------|-------------------------------|
|+  |加 - 两个对象相加               |a + b 输出结果 31                  |
|-  |减 - 得到负数或是一个数减去另一个数      |a - b 输出结果 -11                 |
|*  |乘 - 两个数相乘或是返回一个被重复若干次的字符串|a * b 输出结果 210                 |
|/  |除 - x 除以 y               |b / a 输出结果 2.1                 |
|%  |取模 - 返回除法的余数             |b % a 输出结果 1                   |
|** |幂 - 返回x的y次幂              |a**b 为10的21次方                  |
|// |取整除 - 返回商的整数部分           |9//2 输出结果 4 , 9.0//2.0 输出结果 4.0|

### 比较运算符

|运算符|描述                                                                   |实例                |
|---|---------------------------------------------------------------------|------------------|
|== |等于 - 比较对象是否相等                                                        |(a == b) 返回 False。|
|!= |不等于 - 比较两个对象是否不相等                                                    |(a != b) 返回 true. |
|>  |大于 - 返回x是否大于y                                                        |(a > b) 返回 False。 |
|<  |小于 - 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。|(a < b) 返回 true。  |
|>= |大于等于 - 返回x是否大于等于y。                                                   |(a >= b) 返回 False。|
|<= |小于等于 - 返回x是否小于等于y。                                                   |(a <= b) 返回 true。 |

### Python赋值运算符

|运算符|描述      |实例                          |
|---|--------|----------------------------|
|=  |简单的赋值运算符|c = a + b 将 a + b 的运算结果赋值为 c|
|+= |加法赋值运算符 |c += a 等效于 c = c + a        |
|-= |减法赋值运算符 |c -= a 等效于 c = c - a        |
|*= |乘法赋值运算符 |c *= a 等效于 c = c * a        |
|/= |除法赋值运算符 |c /= a 等效于 c = c / a        |
|%= |取模赋值运算符 |c %= a 等效于 c = c % a        |
|**=|幂赋值运算符  |c **= a 等效于 c = c ** a      |
|//=|取整除赋值运算符|c //= a 等效于 c = c // a      |

### Python位运算符
按位运算符是把数字看作二进制来进行计算的。Python中的按位运算法则如下：
下表中变量 a 为 60，b 为 13。

|运算符|描述                                                |实例                                                |
|---|--------------------------------------------------|--------------------------------------------------|
|&  |按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0          |(a & b) 输出结果 12 ，二进制解释： 0000 1100                 |
|&#124;|  按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。                   |(a&#124;b) 输出结果 61 ，二进制解释： 0011 1101                 |
|^  |按位异或运算符：当两对应的二进位相异时，结果为1                          |(a ^ b) 输出结果 49 ，二进制解释： 0011 0001                 |
|~  |按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1                 |(~a ) 输出结果 -61 ，二进制解释： 1100 0011， 在一个有符号二进制数的补码形式。|
|<< |左移动运算符：运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。|a << 2 输出结果 240 ，二进制解释： 1111 0000                 |
|\>> |右移动运算符：把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数    |a >> 2 输出结果 15 ，二进制解释： 0000 1111                  |

### Python逻辑运算符
Python语言支持逻辑运算符，以下假设变量 a 为 10, b为 20:

|运算符|逻辑表达式  |描述                                                  |实例                   |
|---|-------|----------------------------------------------------|---------------------|
|and|x and y|布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。 |(a and b) 返回 20。     |
|or |x or y |布尔"或" - 如果 x 是 True，它返回 True，否则它返回 y 的计算值。          |(a or b) 返回 10。      |
|not|not x  |布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。|not(a and b) 返回 False|


### Python成员运算符
除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。

|运算符   |描述                               |实例                                |
|------|---------------------------------|----------------------------------|
|in    |如果在指定的序列中找到值返回 True，否则返回 False。  |x 在 y 序列中 , 如果 x 在 y 序列中返回 True。  |
|not in|如果在指定的序列中没有找到值返回 True，否则返回 False。|x 不在 y 序列中 , 如果 x 不在 y 序列中返回 True。|

### Python身份运算符
身份运算符用于比较两个对象的存储单元。

|运算符   |描述                      |实例                                           |
|------|------------------------|---------------------------------------------|
|is    |is是判断两个标识符是不是引用自一个对象    |x is y, 如果 id(x)  等于 id(y) , is 返回结果 1       |
|is not|is not是判断两个标识符是不是引用自不同对象|x is not y, 如果 id(x) 不等于 id(y). is not 返回结果 1|


### Python运算符优先级
以下表格列出了从最高到最低优先级的所有运算符：

|运算符                     |描述                               |
|------------------------|---------------------------------|
|**                      |指数 (最高优先级)                       |
|~ + -                   |按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)|
|* / % //                |乘，除，取模和取整除                       |
|+ -                     |加法减法                             |
|>> <<                   |右移，左移运算符                         |
|&                       |位 'AND'                          |
|^ |                     位运算符                             |
|<= < > >=               |比较运算符                            |
|<> == !=                |等于运算符                            |
|= %= /= //= -= += *= **=|赋值运算符                            |
|is is not               |身份运算符                            |
|in not in               |成员运算符                            |
|not or and              |逻辑运算符                            |

## 参考
[1]. http://www.runoob.com/python3
