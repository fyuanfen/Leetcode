---
title: leetcode21- Merge Two Sorted Lists
date: 2016-08-17 20:31:22
categories: 
- Code
tags:
- Leetcode
---

# Merge Two Sorted Lists
## Describe:
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.
## Solution1:
合并两个有序链表，这里为了统一操作，我用了一个head结点，依次比较l1和l2的值
## Code1:
```java
   public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
       	ListNode head ,p;
       	head =new  ListNode(0);
		p=head;
       	while(l1!=null&&l2!=null){
        if (l1.val >=l2.val){
            p.next = l2;
            l2=l2.next;     
        }  
        
        else{
            p.next = l1;
            l1=l1.next;             
            }  
            p=p.next;
        }
        
        if(l2==null){
             p.next = l1;
        }
       else{
            p.next=l2;
        }   
          return head.next;        
   }
``` 

## Solution2:
这里还看到一种递归解法 ，更简练一些

## Code2: 
```java
   public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if (l1 == null) return l2;
    if (l2 == null) return l1;
    ListNode head = l1.val < l2.val ? l1 : l2;
    ListNode nonHead = l1.val < l2.val ? l2 : l1;
    
    head.next = mergeTwoLists(head.next, nonHead);
    
    return head;
}