---
title: Leetcode-9-Palindrome Number
date: 2016-08-14 10:35:41
categories: 
- Code
tags:
- Leetcode


---

# Palindrome Number

## Describe:
Determine whether an integer is a palindrome. Do this without extra space.


同系列题目:

回文数字[**Palindrome Number**](http://zyy1314.com/2016/08/14/leetcode9/)

回文链表[**Palindrome Linked List**](http://zyy1314.com/2016/08/14/leetcode234/)

回文字符串[**Valid Palindrome **](http://zyy1314.com/2016/08/14/leetcode125/)

## Solution:
判断整数是不是回文数，这里要注意溢出问题。
还有不能把整数转为字符串，因为要求不能使用额外的空间


```java
   public boolean isPalindrome(int x) {
		 if (x%10==0&&x!=0) return false;
		
		 int rev = 0;
		 while(x>rev){
		 rev= rev*10 + x%10;
		 x=x/10;
		 }
		 
		 if (x==rev||x==rev/10){
			 return true;
		 }
		 return false;
	    }
   ```