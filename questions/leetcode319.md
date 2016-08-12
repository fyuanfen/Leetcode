---
title: Leetcode-319-Bulb Switcher
date: 2016-08-12 09:35:24
categories: 
- Code
tags:
- Leetcode

---

# Bulb Switcher

## Describe:
There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.



Example:

Given n = 3. 

At first, the three bulbs are [off, off, off].
After first round, the three bulbs are [on, on, on].
After second round, the three bulbs are [on, off, on].
After third round, the three bulbs are [on, off, off]. 

So you should return 1, because there is only one bulb is on.

## Solution:
由上题可知：

灯泡初始状态为 off

第1轮把所有灯泡设为on

第2轮把编码为2的倍数的灯泡设为相反状态，即2，4，6...

第3轮把编码为3的倍数的灯泡设为相反状态，即3，6，9...

Okay，现在操作流程知道了，以下是解题思路：

1. 把每个灯泡从1到n编号，every second bulb 指的是 2, 4, 6, 8, ... 所有小于n的偶数;every third bulb 即3, 6, 9, 12, ... 所有小于n的3的倍数，以此类推;

2. 如果这个灯泡可以被开关偶数次，那么它最后就是灭的；如果被开关奇数次，那么它最后就是亮的。

那么什么位置上的灯泡可以被开关奇数次呢？ 
考虑一个非平方数，如15，它的约数是1,3,5,15。发现没，它的约数是对称存在的！这个时候它最后只会被开关偶数次！但是对于一个平方数，如16，它的约数是1,2,4,8,16。也只有这样的平方数才能最后被开关奇数次！

所以我们的目的就是找出n以内有几个完全平方数。这一点就没什么问题了，直接开平方就行！

## Code:
```java
int bulbSwitch(int n) {
        return (int)Math.sqrt(n);
```