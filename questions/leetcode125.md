---
title: Leetcode-125-Valid Palindrome 
date: 2016-08-13 17:51:56
categories: 
- Code
tags:
- Leetcode

---
# Valid Palindrome 

## Describe:

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.

同系列题目:

回文数字[**Palindrome Number**](http://zyy1314.com/2016/08/14/leetcode9/)

回文链表[**Palindrome Linked List**](http://zyy1314.com/2016/08/14/leetcode234/)

回文字符串[**Valid Palindrome **](http://zyy1314.com/2016/08/14/leetcode125/)

## Solution:


判断一个字符串是不是回文的，忽略大小写。仅考虑字母和数字，不考虑标点符号什么的

## Code:

```python
def isPalindrome(self, s):
    l, r = 0, len(s)-1
    while l < r:
        while l < r and not s[l].isalnum():
            l += 1
        while l <r and not s[r].isalnum():
            r -= 1
        if s[l].lower() != s[r].lower():
            return False
        l +=1; r -= 1
    return True
 ```