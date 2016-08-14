---
title: Leetcode-191-Number of 1 Bits 
date: 2016-08-13 08:20:33
categories: 
- Code
tags:
- Leetcode

---
# Number of 1 Bits 
## Describe:
Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

## Solution:
统计一个数字的二进制格式的1的数目
可参考[**Reverse Bits**](http://zyy1314.com/2016/08/13/leetcode190/)

[**Counting Bits**](http://zyy1314.com/2016/08/13/leetcode338/)统计小于n的每个数字二进制格式中的1的个数

## Code:
```java
    public int hammingWeight(int n) {
        int result=0;
        while(n!= 0){
            result = result + (n&1);
            n = n>>>1;
        }
        return result;
    }
```