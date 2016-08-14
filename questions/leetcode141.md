---
title: Leetcode-141-Linked List Cycle
date: 2016-08-14 15:26:02
categories: 
- Code
tags:
- Leetcode

---


# Linked List Cycle
## Describe:
Given a linked list, determine if it has a cycle in it.

Follow up:

Can you solve it without using extra space?

## Solution:

Use two pointers, slow and fast.

slow moves step by step. fast moves two steps at time.

if the Linked List has a cycle slow and fast will meet at some point.

该题进阶版[**Linked List Cycle II**](http://zyy1314.com/2016/08/14/leetcode142/)

## Code:
```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) return false;
         
        ListNode slow= head;
        ListNode fast=head;
        
        while(fast.next!=null && fast.next.next!=null){
            slow=slow.next;
            fast=fast.next.next;
            
            if (slow==fast){
                return true;
            }
            
        }
        return false;
        
    }
}

```