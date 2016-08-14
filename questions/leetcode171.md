---
title: Leetcode-171-Excel Sheet Column Number 
date: 2016-08-14 13:04:12
categories: 
- Code
tags:
- Leetcode

---

# Excel Sheet Column Number 
## Describe:
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    
## Solution:
给定一个Excel列名，返回它对应的整数值
镜像题目：[** Excel Sheet Column Title**](http://zyy1314.com/2016/08/14/leetcode168/)

## Code:
Java:
```java
int result = 0;
for (int i = 0; i < s.length(); result = result * 26 + (s.charAt(i) - 'A' + 1), i++);
return result;
```


Python:
```python
return reduce(lambda x, y : x * 26 + y, [ord(c) - 64 for c in list(s)])
```