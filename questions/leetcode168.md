---
title: Leetcode-168- Excel Sheet Column Title
date: 2016-08-14 11:06:58
categories: 
- Code
tags:
- Leetcode

---

 # Excel Sheet Column Title
 
 ## Describe:
 Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
 ## Solution:
 给定一个整数，返回它对应的Excel列名
 
 镜像题目：[**Excel Sheet Column Number**](http://zyy1314.com/2016/08/14/leetcode171/)
 ## Code:
 Java:
 
```java
return n == 0 ? "" : convertToTitle(--n / 26) + (char)('A' + (n % 26));
```

Python:
```python
return "" if num == 0 else self.convertToTitle((num - 1) / 26) + chr((num - 1) % 26 + ord('A'))
```