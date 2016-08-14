---
title: Leetcode-142-Linked List Cycle II
date: 2016-08-14 15:29:39
categories: 
- Code
tags:
- Leetcode

---

# Linked List Cycle II
## Describe:
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

Note: Do not modify the linked list.

## Solution:

该题基础版[**Linked List Cycle**](http://zyy1314.com/2016/08/14/leetcode141/)

Define two pointers slow and fast. Both start at head node, fast is twice as fast as slow. If it reaches the end it means there is no cycle, otherwise eventually it will eventually catch up to slow pointer somewhere in the cycle.

Let the distance from the first node to the the node where cycle begins be A, and let say the slow pointer travels  A+B. The fast pointer must travel 2A+2B to catch up. The cycle size is N. Full cycle is also how much more fast pointer has traveled than slow pointer at meeting point.

A+B+N = 2A+2B

N=A+B

From our calculation slow pointer traveled exactly full cycle when it meets fast pointer, and since originally it travled A before starting on a cycle, it must travel A to reach the point where cycle begins! We can start another slow pointer at head node, and move both pointers until they meet at the beginning of a cycle.

具体步骤如下：

1. 给定两个指针slow和fast，slow每次移动一步，fast每次移动两步
2. 设链表起始点到环的起始点距离为a，slow指针与fast指针相遇的点到环的起始点距离为b，环的长度为r；

因此slow与fast相遇时，slow移动距离为a+b, fast移动距离为a+nr+b(n为重复绕环的次数)
>a+nr+b=2(a+b)

>nr=a+b

我们知道slow指针与fast相遇时已经走了a+b（也就是nr）的距离，此时它再走a步，就会移动到环的起始点。

因此，我们创建一个新的指针 cur，
cur 从链表起始点移动，slow从a+b的距离开始移动。移动a步之后，cur 与slow会在环的起始点相遇



## Code:
```java
public class Solution {
            public ListNode detectCycle(ListNode head) {
                ListNode slow = head;
                ListNode fast = head;
        
                while (fast!=null && fast.next!=null){
                    fast = fast.next.next;
                    slow = slow.next;
                    
                    if (fast == slow){
                        ListNode cur = head; 
                        while (cur != slow){
                            slow = slow.next;
                            cur = cur.next;
                        }
                        return slow;
                    }
                }
                return null;
            }
        }
        
 ```

