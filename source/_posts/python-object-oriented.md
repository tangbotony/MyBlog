---
title: Python学习（六）之面向对象
date: 2016-04-28 13:53:36
categories: Python
tags:
- 面向对象
- Python
---
![](http://7xsy4k.com2.z0.glb.clouddn.com/L0p2Tk9mb1crai9IRjJOeUVzdmM5d3VEYXBEbTZmT096RVZocEI0clY2K0pqeG0rZE02UzhnPT0.jpg)
Python从设计之初就已经是一门面向对象的语言，正因为如此，在Python中创建一个类和对象是很容易的。本章节我们将详细介绍Python的面向对象编程。
如果你以前没有接触过面向对象的编程语言，那你可能需要先了解一些面向对象语言的一些基本特征，在头脑里头形成一个基本的面向对象的概念，这样有助于你更容易的学习Python的面向对象编程。
接下来我们先来简单的了解下面向对象的一些基本特征。
<!--more-->
# 面向对象技术简介
* 类(Class): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
* 类变量：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
* 数据成员：类变量或者实例变量用于处理类及其实例对象的相关的数据。
* 方法重写：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方* 法的覆盖（override），也称为方法的重写。
* 实例变量：定义在方法中的变量，只作用于当前实例的类。
* 继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
* 实例化：创建一个类的实例，类的具体对象。
* 方法：类中定义的函数。
* 对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

# 类定义
语法格式如下：
```python
class ClassName:
    <statement-1>
    .
    .
    .
    <statement-N>
```
类实例化后，可以使用其属性，实际上，创建一个类之后，可以通过类名访问其属性。

# 类对象
类对象支持两种操作：属性引用和实例化。
属性引用使用和 Python 中所有的属性引用一样的标准语法：obj.name。
类对象创建后，类命名空间中所有的命名都是有效属性名。所以如果类定义是这样:
```python
class Student:
    id = 10

    def __init__(self):
        self.id = 52020219

    def f(self):
        return "Student"

# 实列调用
student = Student()
print(student.id)
print(student.f())

# 通过类名直接调用
print(Student.id)
```
很多类都倾向于将对象创建为有初始状态的。因此类可能会定义一个名为 __init__() 的特殊方法（构造方法），像上面那样。
# 类的方法
在类地内部，使用def关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数self,且为第一个参数:
```python
class Student:
    id = 10
    name = "Tony"
    age = 20

    def __init__(self):
        self.id = 5202021
        self.name="Self"
        self.age =10
        self.weight = 50



    def f(self):
        return "Student"

# 实列调用
student = Student()
print("id:{},name:{},age:{},weight:{}".format(student.id,student.name,student.age,student.weight))
```
如果通过类名直接调用没有显示申明的数据成员是，就会报错，如：
```python
class Student:
    id = 10
    name = "Tony"
    age = 20

    def __init__(self):
        self.id = 5202021
        self.name="Self"
        self.age =10
        self.weight = 50



    def f(self):
        return "Student"

# 实列调用
student = Student()
print("id:{},name:{},age:{},weight:{}".format(student.id,student.name,student.age,student.weight))

# 通过类名直接调用
print(Student.weight)
```
Result:
```bash
/Users/tangbo/.pyenv/versions/3.5.0/bin/python /Users/tangbo/Study/Code/Python/hehe/src/a/Student.py
id:5202021,name:Self,age:10,weight:50
Traceback (most recent call last):
  File "/Users/tangbo/Study/Code/Python/hehe/src/a/Student.py", line 22, in <module>
    print(Student.weight)
AttributeError: type object 'Student' has no attribute 'weight'
```

# 继承
Python 同样支持类的继承，如果一种语言不支持继承就，类就没有什么意义。派生类的定义如下所示:
```python
class DerivedClassName(BaseClassName1):
    <statement-1>
    .
    .
    .
    <statement-N>
```
需要注意圆括号中基类的顺序，若是基类中有相同的方法名，而在子类使用时未指定，python从左至右搜索 即方法在子类中未找到时，从左到右查找基类中是否包含方法。
BaseClassName（示例中的基类名）必须与派生类定义在一个作用域内。除了类，还可以用表达式，基类定义在另一个模块中时这一点非常有用:
```python
class DerivedClassName(modname.BaseClassName):
```
```python
class People:
    id = 10
    name = "people"
    age = 0
    weight = 0

    def __init__(self):
        self.id = 5202021
        self.name = "Self"
        self.age = 10
        self.weight = 50

class Student(People):
    score = 0

    def __init__(self):
        self.score = 750

    def f(self):
        return "Student"

# 实列调用
student = Student()
print("id:{},name:{},age:{},weight:{},score:{}".format(student.id,student.name,student.age,student.weight,student.score))
```

# 多继承
Python同样有限的支持多继承形式。多继承的类定义形如下例:
```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```
需要注意圆括号中父类的顺序，若是父类中有相同的方法名，而在子类使用时未指定，python从左至右搜索 即方法在子类中未找到时，从左到右查找父类中是否包含方法。
```python
class People:
    id = 10
    name = "people"
    age = 0
    weight = 0

    def __init__(self):
        self.id = 5202021
        self.name = "Self"
        self.age = 10
        self.weight = 50

    def speak(self):
        return "Pelple"


class Teenager:
    def speak(self):
        return "teenager"

class Student(People,Teenager):
    score = 0

    def __init__(self):
        self.score = 750


    def f(self):
        return "Student"

# 实列调用
student = Student()
print("id:{},name:{},age:{},weight:{},score:{},speak:{}".format(student.id,student.name,student.age,student.weight,student.score,student.speak()))
```

# 方法重写
如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法，实例如下：
```python
class People:
    def study(self):
        return "People Study!!"

class Student(People):
    def study(self):
        return "Student Study"

student = Student()
print(student.study())
```

# 类属性与方法
类的私有属性
__private_attrs：两个下划线开头，声明该属性为私有，不能在类地外部被使用或直接访问。在类内部的方法中使用时 self.__private_attrs。
类的方法
在类地内部，使用def关键字可以为类定义一个方法，与一般函数定义不同，类方法必须包含参数self,且为第一个参数
类的私有方法
__private_method：两个下划线开头，声明该方法为私有方法，不能在类地外部调用。在类的内部调用 slef.__private_methods。
实例如下：
```python
class People:
    pub = 20
    __inn = 10
    def study(self):
        self.__inn = 30
        self.pub = 30
        return "People Study!!"

student = People()
student.pub
```
```bash
/Users/tangbo/.pyenv/versions/3.5.0/bin/python /Users/tangbo/Study/Code/Python/hehe/src/a/Student.py
Traceback (most recent call last):
  File "/Users/tangbo/Study/Code/Python/hehe/src/a/Student.py", line 11, in <module>
    student.__inn
AttributeError: 'People' object has no attribute '__inn'
```

# 类的专有方法：
* \__init\__ : 构造函数，在生成对象时调用
* \__del\__ : 析构函数，释放对象时使用
* \__repr\__ : 打印，转换
* \__setitem\__ : 按照索引赋值
* \__getitem\__: 按照索引获取值
* \__len\__: 获得长度
* \__cmp\__: 比较运算
* \__call\__: 函数调用
* \__add\__: 加运算
* \__sub\__: 减运算
* \__mul\__: 乘运算
* \__div\__: 除运算
* \__mod\__: 求余运算
* \__pow\__: 称方

# 运算符重载
Python同样支持运算符重载，我么可以对类的专有方法进行重载，实例如下：
```python
class People:
    pub = 20
    __inn = 10
    
    def __abs__(self,other):
        if other>0:
            other = other*(-1)
        return other

people = People()
print(people.__abs__(5))
```
# 参考
[1]. http://www.runoob.com/python3/python3-class.html
