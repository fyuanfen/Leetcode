---
title: Leetcode-2-Add Two Numbers
date: 2016-08-06 10:32:05

categories: 
- Code
tags:
- Leetcode

---


# Add Two Numbers
 
## Describe: 

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8


## Solution:

本题计算两个数字链表的和，且数字是反向存储的。
思路很简单，用两个指针遍历链表，如果链表不为空，则计算两个节点之和。把和的低位保存到result链表中，进位则参与到下一位的加法操作中。
如果有进位，则再计算sum/10与下两个链表节点之和，依次循环
 
本题是十进制加法，还有对应的[**二进制加法**](http://zyy1314.com/2016/08/06/leetcode67/)

[**大数乘法**](http://zyy1314.com/2016/08/07/leetcode43/)




## Code:
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode c1 = l1;
        ListNode c2 = l2;
        ListNode result = new ListNode(0);//结果的头结点
        ListNode d = result;
        int sum = 0;
        while (c1 != null || c2 != null|| sum ==1) {
            sum /= 10;
            if (c1 != null) {
                sum += c1.val;
                c1 = c1.next;
            }
            if (c2 != null) {
                sum += c2.val;
                c2 = c2.next;
            }
            d.next = new ListNode(sum % 10);
            d = d.next;
            sum = sum/10;
        }
      
        return result.next;
    }
```