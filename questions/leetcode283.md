---
title: 	Leetcode-283-Move Zeroes 
date: 2016-08-12 12:55:43
categories: 
- Code
tags:
- Leetcode
---


# Move Zeroes 

## Describe:
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

## Solution:
由于有空间限制，因此将该数组元素不为0的数字先存起来，再存储0元素

## Code:
```java
public void moveZeroes(int[] nums) {
    if (nums == null || nums.length == 0) return;        

    int insertPos = 0;
    for (int num: nums) {
        if (num != 0) nums[insertPos++] = num;
    }        

    while (insertPos < nums.length) {
        nums[insertPos++] = 0;
    }
}


```