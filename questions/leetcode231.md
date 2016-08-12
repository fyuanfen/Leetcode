---
title: Leetcode-231-Power of Two
date: 2016-08-12 10:35:42
categories: 
- Code
tags:
- Leetcode
---

Power of Two
# Describe:
Given an integer, write a function to determine if it is a power of two.
## Solution:
Power of 2 means only one bit of n is '1', so use the trick n&(n-1)==0 to judge whether that is the case
## Code:
```java
public boolean isPowerOfTwo(int n) {
		     return ((n & (n-1))==0 && n>0);
        
    }


```