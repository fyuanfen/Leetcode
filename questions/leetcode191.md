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

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

## Solution:

Java中的位运算符：

`>>`表示右移，如果该数为正，则高位补0，若为负数，则高位补1；

`>>>`表示无符号右移，也叫逻辑右移，即若该数为正，则高位补0，而若该数为负数，则右移后高位同样补0。
这里要使用`>>>`，因为当输入的数为一个负数的时候，比如0x8000-0000，当右移一位变成0x0400-0000，其实不是这样的，因为移位前是一个负数，所以我们要保证移位后的数也是一个负数，因此移位后改数变为0xC000-0000.最高位永远都是1，最终这个数字会变成0xFFFF-FFFF，程序陷入死循环。


统计一个数字的二进制格式的1的数目
可参考[**Reverse Bits**](http://zyy1217.com/2016/08/13/leetcode190/)

[**Counting Bits**](http://zyy1217.com/2016/08/13/leetcode338/)统计小于n的每个数字二进制格式中的1的个数

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