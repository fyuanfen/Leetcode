---
title: Leetcode-23-Merge k Sorted Lists Add to List
date: 2016-04-03 15:46:24
categories: 
- Code
tags:
- Leetcode

---


# Merge k Sorted Lists Add to List


合并k个有序链表
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

使用递归方法，首先使用partition函数将k个有序链表划分为多个子问题，然后分别进行归并排序。

```java
public static ListNode mergeKLists(ListNode[] lists){
    return partion(lists,0,lists.length-1);
}

public static ListNode partion(ListNode[] lists,int s,int e){
    if(s==e)  return lists[s];
    if(s<e){
        int q=(s+e)/2;
        ListNode l1=partion(lists,s,q);
        ListNode l2=partion(lists,q+1,e);
        return merge(l1,l2);
    }else
        return null;
}

//This function is from Merge Two Sorted Lists.
public static ListNode merge(ListNode l1,ListNode l2){
    if(l1==null) return l2;
    if(l2==null) return l1;
    if(l1.val<l2.val){
        l1.next=merge(l1.next,l2);
        return l1;
    }else{
        l2.next=merge(l1,l2.next);
        return l2;
    }
}
```