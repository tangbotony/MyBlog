---
title: 为何这道题通过率如此之低
date: 2016-03-22 10:34:08
categories: Leetcode
tags: 
- Leetcode
- Java
- Algorithm
---
## Problems: String to Integer (atoi)
``` bash
8. String to Integer (atoi) My Submissions Question
Total Accepted: 93678 Total Submissions: 698180 Difficulty: Easy
Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Update (2015-02-10):
The signature of the C++ function had been updated. If you still see your function signature accepts a const char * argument, please click the reload button  to reset your code definition.

spoilers alert... click to show requirements for atoi.

Requirements for atoi:
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.
```
## Result 
``` bash
8	String to Integer (atoi)	13.4%	Easy
```
<!-- more -->
终于刷完Easy模式的所有题目了。上面这道题是LeetCode Easy模式里面通过率最低的一道，但是感觉这道题目不是最难的啊，而且边界判断还没有7. Reverse Integer多，真是奇怪啊...
## Solution
``` Java
public class Solution {
    public int myAtoi(String str) {
    	int result;
        String formal = "";
        boolean flag = false;//用来判断是否超出边界
        for(int i =0; i<str.length(); i++)
        {
            if(str.charAt(i)>='0' && str.charAt(i)<='9' || (str.charAt(i)=='-' && formal.length()==0)||(str.charAt(i)=='+' && formal.length()==0))
            {
            	if(str.charAt(i)>'0' && str.charAt(i)<'9')//判断formal字符串里面是否有不为0的数字，用来判断是否越界
            		flag = true;
            	formal = formal+ str.charAt(i);
            }else
            	if(!(str.charAt(i)==' ' && formal.length()==0))//只有前面的空格需要过滤掉
            		break;
        }
        try {
        	result = Integer.parseInt(formal);
		} catch (Exception e) {
			result = 0;
		}
        if(flag && result==0)//如果formal里面有不为0的数字，结果却为0，只能说明越界了
        	if(formal.charAt(0)=='-')
        		result = Integer.MIN_VALUE;
        	else
        		result = Integer.MAX_VALUE;
        return result;
    }
}
```
## Spring comes
{% img /images/20160322/spring_comes.jpg%}
