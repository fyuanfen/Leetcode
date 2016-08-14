---
title: Leetcode190-Reverse Bits
date: 2016-08-12 21:43:27
categories: 
- Code
tags:
- Leetcode

---

# Reverse Bits
## Describe: 
Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).


## Solution:

1. 首先将n和1按位与，获得n的二进制第i位的值
2. 将它赋值给result，同时把result左移一位
3. 再将n右移一位，重复进行上述操作
同系列题目[**Number of 1 Bits **](http://zyy1314.com/2016/08/13/leetcode191/)
[**Counting Bits**](http://zyy1314.com/2016/08/13/leetcode338/)统计小于n的每个数字二进制格式中的1的个数
# Code:
```java
public int reverseBits(int n) {
		  int result = 0;
		  for (int i = 0; i < 32; ++i) {
		    result = result<<1  | (n & 1);//判断n的第i位是否为1
		    n >>>= 1;//无符号右移一位
		  }
		return result; 
		
	 }
         
```