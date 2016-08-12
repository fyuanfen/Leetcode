---
title: Leetcode-67-Add Binary
date: 2016-08-06 15:06:35
categories: 
- Code
tags:
- Leetcode

---

# Add Binary

## Describe: 
Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".

## Solution:


1. 从字符串a和b的最低位开始，返回字符串的索引对应的char值，并进行累加
2. 字符串的每一个位都要进行一次加法操作，把每次累加的结果的低位数字转换为字符存储到字符串builder中
3. 判断每一次操作是否有进位，本题因为是执行二进制加法，因此大于1即进位。c保存进位的值，进行下一次累加操作
4. 循环执行上述操作
5. 注意因为计算顺序是从低位到高位，所以输出时需要reverse一下


本题是二进制加法，还有对应的[**十进制加法**](http://zyy1314.com/2016/08/06/leetcode2/)


[**大数乘法**](http://zyy1314.com/2016/08/07/leetcode43/)


## Code:



```java
public String addBinary(String a, String b) {
    if(a == null || a.length() == 0) return b;
    if(b == null || b.length() == 0) return a;
        
    StringBuilder builder = new StringBuilder();
    int i = a.length() - 1, j = b.length() - 1, c = 0;
         
    while(i >= 0 || j >= 0 || c == 1) {
        c += i >= 0 ? a.charAt(i --) - '0' : 0;
        c += j >= 0 ? b.charAt(j --) - '0' : 0;
            
        builder.append((char) ('0' + c % 2));
        c = c > 1 ? 1 : 0;
    }
    return builder.reverse().toString();
}
    }
```