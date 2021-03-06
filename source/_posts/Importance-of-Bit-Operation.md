---
title: 论位操作的重要性
date: 2016-03-27 21:19:24
categories: Java
tags: 
- Java
- Leetcode
- Algorithm
- 位操作
---
随着Leetcode刷题计划的推进，发现位操作越发的重要，很多时候甚至是离开了位操作运算，你压根就没法解决这个问题。熟练使用位操作会让你有事半功倍的效果，那下面我们就来看看位操作是如何事半功倍的。
## 为什么要学习位操作运算
***
### 从一些小的列子说起
1.交换两个变量的值，传统的方法是这样
``` java
	temp = a; 
	a = b; 
	b = temp;
```
但是，我现在的要求是不能采用任何的额外变量，那该怎么做呢？

2.求两个数的平均数。一般的做法是
``` java
return (x+y)/2;
```
但是上面的代码是有问题的，你也许会说我一直就是这么写的，从来没有出过问题啊，那么我只能说你没遇到，当x+y大于Integer.MAX_VALUE(2147483647)的时，这个求解方法就是错的，那该怎么做呢？

3.判断一个整数是不是2的幂。一般情况下，我们会这么写
``` java
while(p%2==0){
    p=p/2;
}
```
但是上面这种方法效率太低了，其实我们利用位操作一行代码就可以解决。再给出上面几个问题的答案之前，先来温习一些简单的位操作基础知识。
<!-- more -->
## 位操作基础
***
### java 数的表示形式

在了解位移之前，先了解一下正数和负数的二进制表示形式以及关系：
正数 就等于原码
负数 正数的原码取反，再加1。
``` bash
举例15和-15：
 15的原码: 00000000 00000000 00000000 00001111 
-15的原码: 10000000 00000000 00000000 00001111
          11111111 11111111 11111111 11110000
	 +                                  1
-15的补码= 11111111 11111111 11111111 11110001
```

**注意事项**

* Java中没有无符号数，换言之，Java中的数都是有符号，除了char类型，char是无符号的
* 二进制的最高位是符号位，0表示正数，1表示负数
* 正数的原码，反码，补码都一样
* 负数的反码 = 它的原码符号位不变，其他位取反
* 负数的补码 = 它的反码+1
* 0的反码，补码都是0

### java的基本位操作符

| 序号  | 逻辑运算符 | 描述 |
|------|:---------:|-----:|
|   1  |  &        |按位与 |
|   2  | \|        按位或 |
|   3  |   ~        |按位非 | 
|   4  |  ^        |按位异或 |
|   5  |  >>        |右移 |
|   6  |  <<        |左移 |
|   7  |  >>>        |无符号右移 |

& 与操作  规则：仅当两个操作数都为1时，输出的结果才为1，否则为0。
``` bash
 a = 136，b = 129，则a & b 的运算结果如下：
          136    1000 1000    a数
    &     129    1000 0001    b数
    =            1000 0000
```
通常我们可把按位“与”操作 & 作为关闭某位（即将该位置0）的手段，例如我们想要关闭a数中的第3位，而又不影响其它位的现状，可以用一个数247，即二进制数1111 0111去与a数作按位“与”运算：
``` bash
        136    1000 1000    a数
    &   247    1111 0111    屏蔽数
    =          1000 0000
```

| 或操作  规则：仅当两个操作数都为0时，输出的结果才为0，否则为1。
``` bash
    a = 0x88，b = 0x81，则a | b 的运算结果如下：
        136    1000 1000    a数
    |   129    1000 0001    b数
    =          1000 1001
```

~ 非操作  规则：所有的0置为1，1置为0。
``` bash
	a = 0x88 则 ~a 的结果如下
		136    1000 1000    a数
	~
	=              0111 0111
```

^ 异或操作  规则：仅当两个操作数不同时，相应的输出结果才为1，否则为0。
``` bash
  a = 136，b = 129，则a ^ b 的运算结果如下：
        136    1000 1000    a
    ^   129    1000 0001    b
    =          0000 1001
```

**异或操作有一条很重要的性质就是  a^a =0; a^b^a = b; 这条性质我们在后面会用到，具有神奇效果**

\>> 右移操作  规则：m>>n 把整数m表示的二进制数右移n位，m为正数，高位全部补0；m为负数，高位全部补1。
``` bash
  3>>2剖析：
  3二进制形式: 
  00000000 00000000 00000000 00000011
  向右移动两位得到：
  00000000 00000000 00000000 00000000
  即为：0（由于java里面int是32位的，所以表示为这个格式，上面几个列子中由于不涉及到高位，为了简写，所以32位没有写全）
  -3>>2剖析：
  -3二进制形式: 
  11111111 11111111 11111111 11111101
  向右移动两位得到：
  11111111 11111111 11111111 11111111
  即为：-1。
```

<< 左移操作  规则：m &lt; &lt; n 把整数m表示的二进制数左移n位，高位移出n位都舍弃，低位补0。(此时将会出现正数变成负数的形式)
``` bash
  3<<2剖析：
  3二进制形式: 
  00000000 00000000 00000000 00000011
  向左移动俩位得到：
  00000000 00000000 00000000 00001100
  即为：12. 
  左移使整数变为负数:
  10737418<<8
  10737418二进制表示形式:
  00000000 10100011 11010111 00001010
  向左移动两位得到：
  10100011 11010111 00001010 00000000
  即为:-1546188288.
```

\>>> 无符号右移操作  规则：整数m表示的二进制右移n位，不论正负数，高位都补零。
``` bash
  3>>>2剖析：
  3二进制形式: 
  00000000 00000000 00000000 00000011
  无符号右移两位得到
  00000000 00000000 00000000 00000000
  即为:0
  -3>>>2剖析：
  -3二进制形式: 
  11111111 11111111 11111111 11111101
  无符号右移两位得到:
  00111111 11111111 11111111 11111111
  即为:1073741823.
```

可能有人会问，左移和右移都有，为什么有无符号右移，没有无符号左移? 上网找了一下都没有太规范的解释，我觉得下面这个解释我比较赞同，也比较符合我的想法。
> 因为左移是在后面补0，而右移是在前面边补1或0，有无符号是取决于数的前面的第一位是0还是1，所以右移是会产生到底补1还是0的问题，而左移始终是在右边补，不会产生符号问题，所以没有必要无符号左移<<<，无符号左移<<<和左移<<是一样的概念。

## 位操作的神奇效果
***
讲完位操作的基础后，我们就先来看看如何用位操作优雅的解决上面的问题。

1.交换两个变量的值，不使用中间变量
在上面我们讲异或操作的时候说他有一个性质，就是a^b^a = b，再加上这条性质a^0=a，就可以解决这个问题了。
``` java
void swap(int x , int y)  
{  
    x ^= y;//x = x ^ y;  
    y ^= x;// y = x ^ y; 
    x ^= y;// x = x ^ y;
} 
```

2.求两个数的平均数，代码如下
``` java
int average(int x, int y)   //返回X、Y的平均值  
{     
     return (x & y) + ( (x^y)>>1 );  
}
```
上面的代码如何理解呢？我们可以想象一下a和b按照位整齐排序，当a和b对应为上全为1的时候，相加会使此位为0，并且会向前进一位，所以当出现对应位全为1的时候，直接在此位保留一个1就算对这两个对应位求平均值了。然后剩下就是对应位不全为1的时候，分为a的某一个位为1，对应的b的那个位为0，或者倒过来，或者两个都为0，这个时候就要把他们除以2（右移1位）了，然后再相加就行了。

3.判断一个整数是不是2的幂。
思路：如果一个数可以表示为2的n次幂，那么这个数的二进制就只有第n位（从右数起）为1，其它位置都为0，减1以后，那么右边的n-1位都是1，两个值相与一定等于0。
``` bash
以4(100)、7(0111)、8(1000)为例
4&3 --> 100&011 = 0
7&6 --> 0111&0110 != 0
8&7 --> 1000&0111 = 0
```
``` java
boolean power2(int x)  
{  
    return ( (x&(x-1))==0) && (x!=0);  
}  
```

## Leetcode题目运用
***
下面用三个Leetcode的题目来说明位操作的精彩运用。





> 190. Reverse Bits.   
Reverse bits of a given 32 bits unsigned integer.  
For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).  
Follow up:  
If this function is called many times, how would you optimize it?

题目要求将一个整数的二进制翻转，如0x00000001 翻转成0x10000000。这个与10进的翻转类似。然后我们的思路就是不断的提取最右边的一位，然后左移。 
``` java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int result = 0;
        for(int i=0;i<32;i++)
        {
            result<<=1;//左移
            if((n&1)==1)//判断最后一位是不是1，如果是1给result加1
                result |=1;
            n>>>=1;//然后将最后一位移除
        }
        return result;
    }
}
```
当然你也可以利用java自带的函数一句话解决上面的问题：
``` java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
    	return Integer.reverse(n);
    }
}
```

> 136. Single Number.  
Given an array of integers, every element appears twice except for one. Find that single one.  
Note:  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

这道题简直就是逆天，implement it without using extra memory and linear runtime complexity，想了两天根本想不到解决方案啊，无奈只有上网看解决方案。看完后感叹这TMD不会是正常的，竟然使用异或操作，根本没有想到异或操作还有如此大用，想当时上C语言的时候，关于异或操作，老师一句话就给我们讲完了，那就是这部分大家自己下去看啊。废话不多说，先上代码：
``` java
public class Solution {
    public int singleNumber(int[] nums) {
        int result=0;
        for(int n : nums)
            result^=n;
        return result;
    }
}
```
代码相当的简洁，其实就是利用到上面异或操作的性质 a^b^a = b;这样就把只出现一次的那个数给找出来了。
> 260. Single Number III  
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.  
For example:  
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].  
Note:  
The order of the result is not important. So in the above example, [5, 3] is also correct.  
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

这个题目和上一个题目很像，但是我敢打赌，就算你理解上一道题目的精华，在不借助外援的情况下，你也很难想出这道题目怎么做，原谅我这么直白。采用上题的方法，我们也只能想到result的结果是这两个数异或的结果，就很难想到我们可以利用这个结果把这两个不同的数给分拆出来。那下面我们就来看看如何利用异或的结果把这两个数分拆出来。
``` 
result = a ^ b;
```
**当a和b不同的时候，必然有一位上a和b一个是0，一个是1，然后根据result出现1这一位将整个数组分成两组，这样我们就把a和b分到两个数组中，然后每一个数组里面就只有一个数出现一次了，在采用上一题的算法就可以得出两个不同的数了。**代码如下：
``` java
public class Solution {
    public int[] singleNumber(int[] nums) {
        int result[] = new int[2];
        int re = 0;
        for(int i : nums)
            re ^= i;
        int n = re & (~(re-1));//得到re从右起第一个出现1的位置所对应的数
        for(int i : nums)
            if((i & n) == 0)
                result[0] ^= i;
            else
                result[1] ^= i;
        return result;
    }
}
```
## 参考
[1]. http://blog.csdn.net/dc_726/article/details/7036533
[2]. http://blog.csdn.net/zhaoweixing1989/article/details/8052261
[3]. http://6url.cn/ckF
{% fullimage  /images/20160323/c.jpg %}
