---
title: Leetcode-234-Palindrome Linked List
date: 2016-08-13 15:46:24
categories: 
- Code
tags:
- Leetcode

---


# Palindrome Linked List
## Describe:
Given a singly linked list, determine if it is a palindrome.


同系列题目:

回文数字[**Palindrome Number**](http://zyy1314.com/2016/08/14/leetcode9/)

回文链表[**Palindrome Linked List**](http://zyy1314.com/2016/08/14/leetcode234/)

回文字符串[**Valid Palindrome **](http://zyy1314.com/2016/08/14/leetcode125/)


## Solution:
给定一个单链表，判断它是不是回文链表，也就是说它的元素是不是首尾对称的。

解题思路是把单链表分为l1和l2两部分，对l1进行反转操作，比较l1和l2是否相同

slow每移动一步，fast指针移动两步。当fast指针移到链表末尾时，slow指向链表的中间



## Code:
```java
public class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null) {
            return true;
        }
        ListNode cur = head;
        ListNode fast = head;
        ListNode slow = cur.next;
        ListNode pre = cur;
        //find mid pointer, and reverse head half part
        while(fast.next  && fast.next.next) {
            fast = fast.next.next;
            pre = cur;
            cur = slow;
            slow = slow.next;
            cur.next = pre;
        }

        //odd number of elements, need left move p1 one step
        if(fast.next == null) {
            cur = cur.next;
        }
        else {   //even number of elements, do nothing
            
        }
        //compare from mid to head/tail
        while( slow != null) {
            if(cur.val != slow.val) {
                return false;
            }
            cur = cur.next;
            slow =  slow.next;
        }
        return true;
        
    }
}
```

## Solution1:
还有python的解法，与上面的原理类似，
只是python在反转链表时更加简练
仅使用` rev,rev.next,slow= slow,rev,slow.next`一条语句即可，具体原理可参考[**python笔记之swap操作**](http://zyy1314.com/2016/08/13/python%E7%AC%94%E8%AE%B0%E4%B9%8Bswap%E6%93%8D%E4%BD%9C/)

## Code１:
```python
 def isPalindrome(self, head):
        rev=None
        slow = fast = head
        
        while(fast and fast.next):
            fast=fast.next.next
            rev,rev.next,slow= slow,rev,slow.next
        if fast:
            slow=slow.next
            
        while (rev and rev.val==slow.val ):
            rev=rev.next
            slow=slow.next
        
        return not rev
    
  ```
## Solution 2: Play Nice

Same as the above, but while comparing the two halves, restore the list to its original state by reversing the first half back. Not that the OJ or anyone else cares.
在反转链表之后，还是要把它转回来的嘛，自己弄得烂摊子要收拾好~
这个要优雅的多


## Code2：
```python
def isPalindrome(self, head):
    rev = None
    fast = head
    while fast and fast.next:
        fast = fast.next.next
        rev, rev.next, head = head, rev, head.next
    tail = head.next if fast else head
    isPali = True
    while rev:
        isPali = isPali and rev.val == tail.val
        head, head.next, rev = rev, head, rev.next
        tail = tail.next
    return isPali
    
    
 ```