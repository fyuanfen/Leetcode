---
title: Leetcode-19-Remove Nth Node From End of List
date: 2017-04-10 22:23:52
categories: 
- Code
tags:
- Leetcode

---




Given a linked list, remove the nth node from the end of list and return its head.

For example,

```
   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
```

**Note:**

Given n will always be valid.
Try to do this in one pass.


倒数第k个结点和倒数第1个结点相隔k-1个
## 解题思路：
其实前面的解题思路和[]一样，只不过有一丢丢小区别。
![](http://images.zyy1217.com/IMG_4561.jpg)

为了方便理解，我画了一个图：

1. 初始化的时候，p,q都指向第一个结点。

2. 然后q向前走n步，p保持不动
3. 由于两个指针的距离保持在n，当第一个（走在前面的）指针到达链表尾结点的下一个结点（也就是倒数第0个结点，即null值）时，第二个指针（走在后面的）指针正好是倒数第n个结点。

这里要注意以下几点：

1. 为了删除倒数第k个结点，我们需要找到他的前一个结点，也就是倒数第k+1个结点。

2. 因为可能存在倒数第k个结点就是head的情况，那么就不存在倒数第k+1个结点的情况。因此，为了避免考虑删除head结点和普通结点的不同操作，我们设了一个dummy head。



```java
public class Solution {
    public ListNode removeNthFromEnd(ListNode head, int k) {
        ListNode start = new ListNode(0);
        start.next = head;
        ListNode p = start;
        ListNode q = start;
        
        int count = 0;
        while(q != null && count < k+1) {//第一个指针移动k+1次
            q = q.next;
            count++;
        }     
        if(count == k+1) {// 如果成功移动了k+1次
            while(q != null) { 
                p = p.next;
                q = q.next;
            }
            //删除倒数第k+1个指针p后面的结点
            p.next = p.next.next;
        }
        return start.next;
    }
}
```