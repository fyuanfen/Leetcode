
# Reverse Linked List
## Describe: 
Reverse a singly linked list.
## Solution:
A linked list can be reversed either iteratively or recursively.
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