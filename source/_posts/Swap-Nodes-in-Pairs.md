
---
title: Swap Nodes in Pairs
date: 2016-03-23 19:34:29
categories: Leetcode
tags:
 - Leetcode 
 - Java 
 - Algorithm
---
这道题还是第一次在Leetcode的输入框里面写完代码，一次Submit Solution后，直接通过的，证明这段时间用Sublime Text 写代码，不用IDE，提升还是很显著的。
``` bash
24. Swap Nodes in Pairs My Submissions Question
Total Accepted: 87086 Total Submissions: 249646 Difficulty: Easy
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given 1->2->3->4, you should return the list as 2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

```
### 解题思路
1. 对于头结点单独交换
``` java
ListNode tempNode = head;
head = head.next;
tempNode.next = head.next;
head.next = tempNode;
```
<!-- more -->
2. 对于其它的节点采用如下的交换方式
{% img /images/20160323/a.png %}
``` java
beforNode.next = nextNode;
tempNode.next = nextNode.next;
nextNode.next = tempNode;
```
3. 交换后，重新设定beforNode,tempNode的值
{% img /images/20160323/b.png %}
``` java
beforNode = tempNode;
tempNode = tempNode.next;
```
### AC的代码
``` java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head==null || head.next == null)
            return head;
        //对头结点单独处理
        ListNode tempNode = head;
        head = head.next;
        tempNode.next = head.next;
        head.next = tempNode;
        //头结点交换结束，准备后面的交换
        ListNode beforNode =head.next;
        tempNode = beforNode.next;
        ListNode nextNode;
        while(tempNode!=null)
        {
            if(tempNode.next==null)//证明只有一个节点了，不需要交换
                break;
            nextNode = tempNode.next;
            beforNode.next = nextNode;
            tempNode.next = nextNode.next;
            nextNode.next = tempNode;
            beforNode = tempNode;
            tempNode = tempNode.next;
        }
        return head;
    }
}
```
{% img  /images/20160323/d.jpg %}
