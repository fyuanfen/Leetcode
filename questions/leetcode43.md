---
title: Leetcode-43-Multiply Strings 
date: 2016-08-07 09:20:02
categories: 
- Code
tags:
- Leetcode

---

# Multiply Strings 
## Describe:  
Given two numbers represented as strings, return multiplication of the numbers as a string.

**Note:
The numbers can be arbitrarily large and are non-negative.
Converting the input string to integer is NOT allowed.
You should NOT use internal library such as BigInteger.
**


## Solution:


Start from right to left, perform multiplication on every pair of digits, and add them together. Let's draw the process! From the following draft, we can immediately conclude:


`num1[i] * num2[j]` will be placed at indices `[i + j`, `i + j + 1]` 
![Multiplication](http://oavk3bisu.bkt.clouddn.com/leetcode1.jpg)

本题的核心思想是，计算`num1[i] * num2[j]`的结果，并放在pos`[i + j`, `i + j + 1]` 上，如上图所示。每轮都要更新pos数组的值

由上图可知,计算流程为：

1. 计算`num1[i] * num2[j]`,高位放pos[i+j]，低位放pos[i+j+1]

2. j - -，计算两个数之积，再加上上一轮计算结果的进位，即pos[p2]。**注意，这里因为j - -，所以pos[p2]指的就是上一轮的pos[p1]，即进位数值**


同系列题目：
[**Add Two Numbers**]
(http://zyy1314.com/2016/08/06/leetcode2/)

[**Add Binary**](http://zyy1314.com/2016/08/06/leetcode67/)

 ## Code:
```java
public String multiply(String num1, String num2) {
    int m = num1.length(), n = num2.length();
    int[] pos = new int[m + n];
   
    for(int i = m - 1; i >= 0; i--) {
        for(int j = n - 1; j >= 0; j--) {
            int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0'); 
            int p1 = i + j, p2 = i + j + 1;
            int sum = mul + pos[p2];//计算乘积与进位之和

            pos[p1] += sum / 10;
            pos[p2] = (sum) % 10;
        }
    }  
    
    StringBuilder sb = new StringBuilder();
    for(int p : pos) if(!(sb.length() == 0 && p == 0)) sb.append(p);
    return sb.length() == 0 ? "0" : sb.toString();
}
```

本题的常规解法为：
# Code2:
```java
public class Solution {
    public String multiply(String num1, String num2) {
        int len1 = num1.length();
        int len2 = num2.length();
        int len = len1 + len2;
        int[] mul = new int[len];
        for (int i = len1 - 1; i >= 0; i--) {
            int a = num1.charAt(i) - '0';
            int k = len2 + i;
            for (int j = len2 - 1; j >= 0; j--) {
                int b = num2.charAt(j) - '0';
                int c = mul[k] + a * b;
                mul[k] = c % 10;
                mul[k - 1] = mul[k - 1] + c /10;
                k--;
            }
        }
        int i = 0;
        while(mul[i] == 0 && i < len - 1)  i++;
        StringBuilder sb = new StringBuilder();
        for (; i < len; i++)
            sb.append(mul[i]);
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```
