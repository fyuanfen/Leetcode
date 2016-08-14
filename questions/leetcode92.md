---
title: Leetcode-92-Reverse Linked List II 
date: 2016-08-02 17:17:14
categories: 
- Code
tags:
- Leetcode

---


# Reverse Linked List II 
## Describe:
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given 1->2->3->4->5->NULL, m = 2 and n = 4,

return 1->4->3->2->5->NULL.


## Solution:
反转整个链表可参考[**Reverse Linked List**](http://zyy1314.com/2016/08/02/leetcode206/)

本题要求把下标范围为[m,n]的节点进行反转，从题例可以看出来，下标从1开始计数。

假设，待反转的[m,n]段节点叫做第二段，待反转的[m,n]段节点的左边的节点叫做第一段，待反转的[m,n]段节点的右边的节点叫做第三段。那么，本题最麻烦的地方时，第一段和第三段可能是空的。当m取值为1，n取值为链表长度length时，这样的情况就会发生。
为了避免分情况讨论，在head节点之前增加了节点(称作dummy)，这是常见的扬长避短的做法。
## Code:
```java
public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode dummy=new ListNode(0);
        dummy.next=head;
        ListNode pre=dummy; //pre is the node before orignal M
        ListNode M=head;    //M is after pre
        
        for(int i=1;i<m;i++){ //Move pre and M to orignal place
            pre=pre.next;
            M=M.next;
        }
        
        for(int i=0;i<n-m;i++){ 
            ListNode current=M.next; //Both pre and M are all fixed, only current is assigned every time to M.next. M is pushed back everytime
            M.next=current.next;     //Move current to the position after pre
            current.next=pre.next;
            pre.next=current;
        }
        
        return dummy.next;
    }
    
```