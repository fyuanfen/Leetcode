
---
title: Leetcode-206-Reverse Linked List
date: 2016-08-02 15:29:02
categories: 
- Code
tags:
- Leetcode

---

# Reverse Linked List

## Describe: 
Reverse a singly linked list.

## Solution:
A linked list can be reversed either iteratively or recursively.

本题要求反转整个单链表，部分反转可参考[Reverse Linked List II](http://zyy1314.com/2016/08/02/leetcode92/)
## Code:
1. iteration
```java
  public ListNode reverseList(ListNode head) {
        
        ListNode newHead = null;
        while(head!=null){
            ListNode next = head.next;
            head.next = newHead;
            newHead = head;
            head = next;
        }
        return newHead;
    }
    
```

```javascript
function ReverseList(pHead)
{
   var p3 = null,
       p2 = pHead;
    while( p2 !==null) {
        p2 = pHead.next;
        pHead.next = p3;
        p3 = pHead;
        pHead = p2;
    }
    return p3;
}
```

2. recursion
```java
public ListNode reverseList(ListNode head) {  
        if(head==null) return null;  
        if(head.next==null) return head;  
          
        ListNode p = head.next;  
        ListNode n = reverseList(p);  
          
        head.next = null;  
        p.next = head;  
        return n;  
    }  
    
```