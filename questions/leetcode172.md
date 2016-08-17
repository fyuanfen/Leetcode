---
title: Leetcode-172-Factorial Trailing Zeroes
date: 2016-08-17 15:27:21
categories: 
- Code
tags:
- Leetcode

---
# Factorial Trailing Zeroes

## Describe:
Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.

## Solution:
求N的阶乘(N!)中的末尾有多少个0?
 
分析:想到这个问题，有人可能第一反应就是现求出N!,然后再根据求出的结果，最后得出N!的末尾有多少个0。但是转念一想，会不会溢出，等等。

其实，从"**那些数相乘可以得到10**"这个角度，问题就变得比较的简单了。

首先考虑，如果N的阶乘为K和10的M次方的乘积，那么N!末尾就有M的0。如果将N的阶乘分解后，那么

N的阶乘可以分解为： 2的X次方，3的Y次方，4的5次Z方，.....的成绩。由于10 = 2 * 5,所以M只能和X和Z有关，每一对2和5相乘就可以得到一个10，于是M = MIN(X,Z),不难看出X大于Z，因为被2整除的频率比被5整除的频率高的多。所以可以把公式简化为**M=Z**.
     
**由上面的分析可以看出，只要计算处Z的值，就可以得到N!末尾0的个数**


## Code:

Z = N/5 + N /(5 * 5) + N/( 5 * 5 * 5).....知道N/(5的K次方)等于0

公式中 N/5表示不大于N的数中能被5整除的数贡献一个5，N/(5 * 5)表示不大于N的数中能被25整除的数再共享一个5....

```java
public int trailingZeroes(int n) {
        int num=0;
        while (n!=0){
        num+= n/5;
        n=n/5;
        }
        return num;
```