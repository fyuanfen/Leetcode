---
title: Leetcode-338-Counting Bits
date: 2016-08-13 09:13:54
categories: 
- Code
tags:
- Leetcode

---

# Counting Bits
## Describe:
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

Follow up:

It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
Space complexity should be O(n).

Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

## Solution:
给定一个数字n，给出0到n的每个数字二进制表示的1的个数
本题还有简单版本[**Number of 1 Bits **](http://zyy1314.com/2016/08/13/leetcode191/)
核心思想是`bit[i]=bit[i/2]+i%2;`
## Code:
```java
public int[] countBits(int num) {
        int[] bit = new int[num+1];
        for (int i=1;i<=num;i++){
            bit[i] = bit[i>>1]+i%2;
            
            
        }
        return bit;
    }
 ```