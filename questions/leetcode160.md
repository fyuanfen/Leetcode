---
title: Leetcode-160-Intersection of Two Linked Lists
date: 2016-08-17 17:52:59
categories: 
- Code
tags:
- Leetcode

---

# Intersection of Two Linked Lists
## Describe:
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```
begin to intersect at node c1.
## Solution:

判断两个单链表的交集，一般解法是算出两个链表的长度，把他们放在相同的起点，同步移动他们，直到他们在交集相遇或者移到末尾。
除此之外，还有个想法很巧妙。

- Step1:Scan both lists
- Step2:For each list once it reaches the end, continue scanning the other list
- Step3:Once the two runner equal to each other, return the position


## Code:
```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode a=  headA;
        ListNode b = headB;
        while(a!=b){
            a = a==null?headB:a.next;
            b = b==null?headA:b.next;
        }
        return a;    
    }
```