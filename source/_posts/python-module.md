---
title: Python学习（五）之 模块
date: 2016-04-25 12:50:16
categories: Python
tags:
- Python
- Module
---
![](http://7xsy4k.com2.z0.glb.qiniucdn.com/2016041502.jpg)
在前面的几个章节中我们脚本上是用 python 解释器来编程，如果你从 Python 解释器退出再进入，那么你定义的所有的方法和变量就都消失了。为此 Python 提供了一个办法，把这些定义存放在文件中，为一些脚本或者交互式的解释器实例使用，这个文件被称为模块。模块是一个包含所有你定义的函数和变量的文件，其后缀名是.py。模块可以被别的程序引入，以使用该模块中的函数等功能。这也是使用 python 标准库的方法。
下面是一个使用 python 标准库中模块的例子。
```python
import sys
for x in sys.argv:
	print(x)
```
<!--more-->
# import 语句
想使用 Python 源文件，只需在另一个源文件里执行 import 语句，语法如下：
```python
import module1[, module2[,... moduleN]
```
当解释器遇到 import 语句，如果模块在当前的搜索路径就会被导入。搜索路径是一个解释器会先进行搜索的所有目录的列表。如想要导入模块 util，需要把命令放在脚本的顶端：
util.py 文件代码为：
```python
def speak(content):
	print(content)
```
导入模块
```python
#!/usr/bin/python3
# Filename: test.py
 
# 导入模块
import util
 
# 现在可以调用模块里包含的函数了
util.speak("Hello Word")
```
一个模块只会被导入一次，不管你执行了多少次import。这样可以防止导入模块被一遍又一遍地执行。当我们使用import语句的时候，Python解释器是怎样找到对应的文件的呢？
这就涉及到Python的搜索路径，搜索路径是由一系列目录名组成的，Python解释器就依次从这些目录中去寻找锁引入的模块。这看起来很像环境变量，事实上，也可以通过定义环境变量的方式来确定搜索路径。搜索路径是在Python编译或安装的时候确定的，安装新的库应该也会修改。搜索路径被存储在sys模块中的path变量，做一个简单的实验，在交互式解释器中，输入以下代码：
```python
import sys
sys.path
```
Result:
```bash
['', '/Users/tangbo/.pyenv/versions/3.5.0/lib/python3.5', '/Users/tangbo/.pyenv/versions/3.5.0/lib/python3.5/plat-darwin', '/Users/tangbo/.pyenv/versions/3.5.0/lib/python3.5/lib-dynload', '/Users/tangbo/.pyenv/versions/3.5.0/lib/python3.5/site-packages']
```
sys.path 输出是一个列表，其中第一项是空串''，代表当前目录（若是从一个脚本中打印出来的话，可以更清楚地看出是哪个目录），亦即我们执行python解释器的目录（对于脚本的话就是运行的脚本所在的目录）。因此若像我一样在当前目录下存在与要引入模块同名的文件，就会把要引入的模块屏蔽掉。了解了搜索路径的概念，就可以在脚本中修改sys.path来引入一些不在搜索路径中的模块。现在，在解释器的当前目录或者 sys.path 中的一个目录里面来创建一个fibo.py的文件，代码如下：
```python
# coding: utf-8
# 斐波那契(fibonacci)数列模块

def fib(n):    # 定义到 n 的斐波那契数列
    a, b = 0, 1
    while b < n:
        print(b)
        print("\n")
        a, b = b, a+b
    print()

def fib2(n): # 返回到 n 的斐波那契数列
    result = []
    a, b = 0, 1
    while b < n:
        result.append(b)
        a, b = b, a+b
    return result
```
然后进入Python解释器，使用下面的命令导入这个模块：
```python
import fibo
```
这样做并没有把直接定义在fibo中的函数名称写入到当前符号表里，只是把模块fibo的名字写到了那里。可以使用模块名称来访问函数：
```python
>>> fibo.fib(1000)
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
>>> fibo.fib2(100)
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
>>> fibo.__name__
'fibo'
```
如果你打算经常使用一个函数，你可以把它赋给一个本地的名称：
```python
>>> fib = fibo.fib
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
## from…import 语句
Python的from语句让你从模块中导入一个指定的部分到当前命名空间中，语法如下：
```python
from modname import name1[, name2[, ... nameN]]
```
例如，要导入模块 fibo 的 fib 函数，使用如下语句：
```python
from fibo import fib
```
这个声明不会把整个fib模块导入到当前的命名空间中，它只会将fib里的fibonacci单个引入到执行这个声明的模块的全局符号表。
## From…import* 语句
把一个模块的所有内容全都导入到当前的命名空间也是可行的，只需使用如下声明：
```python
from modname import *
```
**这提供了一个简单的方法来导入一个模块中的所有项目。然而这种声明不该被过多地使用。
**
# 深入模块
模块除了方法定义，还可以包括可执行的代码。这些代码一般用来初始化这个模块。这些代码只有在第一次被导入时才会被执行。每个模块有各自独立的符号表，在模块内部为所有的函数当作全局符号表来使用。所以，模块的作者可以放心大胆的在模块内部使用这些全局变量，而不用担心把其他用户的全局变量搞花。从另一个方面，当你确实知道你在做什么的话，你也可以通过 modname.itemname 这样的表示法来访问模块内的函数。模块是可以导入其他模块的。在一个模块（或者脚本，或者其他地方）的最前面使用 import 来导入一个模块，当然这只是一个惯例，而不是强制的。被导入的模块的名称将被放入当前操作的模块的符号表中。还有一种导入的方法，可以使用 import 直接把模块内（函数，变量的）名称导入到当前操作模块。比如:
```python
>>> from fibo import fib, fib2
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
这种导入的方法不会把被导入的模块的名称放在当前的字符表中（所以在这个例子里面，fibo 这个名称是没有定义的）。这还有一种方法，可以一次性的把模块中的所有（函数，变量）名称都导入到当前模块的字符表:
```python
>>> from fibo import *
>>> fib(500)
1 1 2 3 5 8 13 21 34 55 89 144 233 377
```
这将把所有的名字都导入进来，但是那些由单一下划线（_）开头的名字不在此例。大多数情况， Python程序员不使用这种方法，因为引入的其它来源的命名，很可能覆盖了已有的定义。

## \__name\__属性
一个模块被另一个程序第一次引入时，其主程序将运行。如果我们想在模块被引入时，模块中的某一程序块不执行，我们可以用\__name\__属性来使该程序块仅在该模块自身运行时执行。
```python
# Filename: using_name.py
if __name__ == '__main__':
   print('程序自身在运行')
else:
   print('我来自另一模块')
```
分别运行下面这两个命令
```python
python using_name.py
import using_name
```
说明： 每个模块都有一个\__name\__属性，当其值是'\__main\__'时，表明该模块自身在运行，否则是被引入。

## dir() 函数
内置的函数 dir() 可以找到模块内定义的所有名称。以一个字符串列表的形式返回:
```python
import hehe.src.a.fibo as fb
import sys
print(dir(fb))
print(dir(sys))
```
Result:
```bash
['__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'fib', 'fib1']

['__displayhook__', '__doc__', '__egginsert', '__excepthook__', '__interactivehook__', '__loader__', '__name__', '__package__', '__plen', '__spec__', '__stderr__', '__stdin__', '__stdout__', '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe', '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv', 'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder', 'call_tracing', 'callstats', 'copyright', 'displayhook', 'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix', 'executable', 'exit', 'flags', 'float_info', 'float_repr_style', 'get_coroutine_wrapper', 'getallocatedblocks', 'getcheckinterval', 'getdefaultencoding', 'getdlopenflags', 'getfilesystemencoding', 'getprofile', 'getrecursionlimit', 'getrefcount', 'getsizeof', 'getswitchinterval', 'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info', 'intern', 'is_finalizing', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path', 'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'set_coroutine_wrapper', 'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit', 'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout', 'thread_info', 'version', 'version_info', 'warnoptions']
Process
```
如果没有给定参数，那么 dir() 函数会罗列出当前定义的所有名称

# 标准模块
Python 本身带着一些标准的模块库，在 Python 库参考文档中将会介绍到（就是后面的"库参考文档"）。有些模块直接被构建在解析器里，这些虽然不是一些语言内置的功能，但是他却能很高效的使用，甚至是系统级调用也没问题。这些组件会根据不同的操作系统进行不同形式的配置，比如 winreg 这个模块就只会提供给 Windows 系统。应该注意到这有一个特别的模块 sys ，它内置在每一个 Python 解析器中。变量 sys.ps1 和 sys.ps2 定义了主提示符和副提示符所对应的字符串:
```python
>>> import sys
>>> sys.ps1
'>>> '
>>> sys.ps2
'... '
>>> sys.ps1 = 'Python: '
Python:print('Yuck!')
Yuck!
Python:
```
# 包
包是一种管理 Python 模块命名空间的形式，采用"点模块名称"。比如一个模块的名称是 A.B， 那么他表示一个包 A中的子模块 B 。就好像使用模块的时候，你不用担心不同模块之间的全局变量相互影响一样，采用点模块名称这种形式也不用担心不同库之间的模块重名的情况。这样不同的作者都可以提供 NumPy 模块，或者是 Python 图形库。不妨假设你想设计一套统一处理声音文件和数据的模块（或者称之为一个"包"）。现存很多种不同的音频文件格式（基本上都是通过后缀名区分的，例如： .wav，:file:.aiff，:file:.au，），所以你需要有一组不断增加的模块，用来在不同的格式之间转换。并且针对这些音频数据，还有很多不同的操作（比如混音，添加回声，增加均衡器功能，创建人造立体声效果），所你还需要一组怎么也写不完的模块来处理这些操作。
这里给出了一种可能的包结构（在分层的文件系统中）:
```python
sound/                          顶层包
      __init__.py               初始化 sound 包
      formats/                  文件格式转换子包
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  声音效果子包
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  filters 子包
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```
在导入一个包的时候，Python 会根据 sys.path 中的目录来寻找这个包中包含的子目录。
目录只有包含一个叫做 \__init\__.py 的文件才会被认作是一个包，主要是为了避免一些滥俗的名字（比如叫做 string）不小心的影响搜索路径中的有效模块。最简单的情况，放一个空的 :file:\__init\__.py就可以了。当然这个文件中也可以包含一些初始化代码或者为（将在后面介绍的） \__all\__变量赋值。用户可以每次只导入一个包里面的特定模块，比如:
```python
import sound.effects.echo
```
这将会导入子模块:mod:song.effects.echo。 他必须使用全名去访问:
```python
sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
```
还有一种导入子模块的方法是:
```python
from sound.effects import echo
```
这同样会导入子模块:mod:echo，并且他不需要那些冗长的前缀，所以他可以这样使用:
```python
echo.echofilter(input, output, delay=0.7, atten=4)
```
还有一种变化就是直接导入一个函数或者变量:
```python
from sound.effects.echo import echofilter
```
同样的，这种方法会导入子模块:mod:echo，并且可以直接使用他的:func:echofilter函数:
```python
echofilter(input, output, delay=0.7, atten=4)
```
注意当使用from package import item这种形式的时候，对应的item既可以是包里面的子模块（子包），或者包里面定义的其他名称，比如函数，类或者变量。import语法会首先把item当作一个包定义的名称，如果没找到，再试图按照一个模块去导入。如果还没找到，恭喜，一个:exc:ImportError 异常被抛出了。反之，如果使用形如import item.subitem.subsubitem这种导入形式，除了最后一项，都必须是包，而最后一项则可以是模块或者是包，但是不可以是类，函数或者变量的名字。

# 从一个包中导入*
设想一下，如果我们使用 from sound.effects import \*会发生什么？Python 会进入文件系统，找到这个包里面所有的子模块，一个一个的把它们都导入进来。但是很不幸，这个方法在 Windows平台上工作的就不是非常好，因为Windows是一个大小写不区分的系统。在这类平台上，没有人敢担保一个叫做 ECHO.py 的文件导入为模块:mod:echo还是:mod:Echo甚至:mod:ECHO。（例如，Windows 95就很讨厌的把每一个文件的首字母大写显示）而且 DOS 的 8+3 命名规则对长模块名称的处理会把问题搞得更纠结。为了解决这个问题，只能烦劳包作者提供一个精确的包的索引了。导入语句遵循如下规则：如果包定义文件 \__init\__.py 存在一个叫做\__all\__ 的列表变量，那么在使用 from package import \* 的时候就把这个列表中的所有名字作为包内容导入。作为包的作者，可别忘了在更新包之后保证 \__all\__ 也更新了啊。你说我就不这么做，我就不使用导入\*这种用法，好吧，没问题，谁让你是老板呢。这里有一个例子，在:file:sounds/effects/\__init\__.py中包含如下代码:
```python
__all__ = ["echo", "surround", "reverse"]
```
这表示当你使用from sound.effects import \*这种用法时，你只会导入包里面这三个子模块。如果\__all\__真的而没有定义，那么使用from sound.effects import \*这种语法的时候，就不会导入包:mod:sound.effects里的任何子模块。他只是把包:mod:sound.effects和它里面定义的所有内容导入进来（可能运行:file:\__init\__.py里定义的初始化代码）。这会把 :file:\__init\__.py里面定义的所有名字导入进来。并且他不会破坏掉我们在这句话之前导入的所有明确指定的模块。看下这部分代码:
```python
import sound.effects.echo
import sound.effects.surround
from sound.effects import *
```
这个例子中，在执行from...import前，包:mod:sound.effects中的echo和surround模块都被导入到当前的命名空间中了。（当然如果定义了\__all\__就更没问题了)
通常我们并不主张使用\*这种方法来导入模块，因为这种方法经常会导致代码的可读性降低。不过这样倒的确是可以省去不少敲键的功夫，而且一些模块都设计成了只能通过特定的方法导入。记住，使用from Package import specific_submodule这种方法永远不会有错。事实上，这也是推荐的方法。除非是你要导入的子模块有可能和其他包的子模块重名。如果在结构中包是一个子包（比如这个例子中对于包:mod:sound来说），而你又想导入兄弟包（同级别的包）你就得使用导入绝对的路径来导入。比如，如果模块:mod:sound.filters.vocoder 要使用包:mod:sound.effects中的模块:mod:echo，你就要写成 from sound.effects import echo。
```python
from . import echo
from .. import formats
from ..filters import equalizer
```
无论是隐式的还是显式的相对导入都是从当前模块开始的。主模块的名字永远是"\__main\__"，一个Python应用程序的主模块，应当总是使用绝对路径引用。包还提供一个额外的属性，:attr:\__path\__。这是一个目录列表，里面每一个包含的目录都有为这个包服务的:file:\__init\__.py，你得在其他:file:\__init\__.py被执行前定义哦。可以修改这个变量，用来影响包含在包里面的模块和子包。这个功能并不常用，一般用来扩展包里面的模块。
# 转载自
[1]. http://www.runoob.com/python3/python3-module.html