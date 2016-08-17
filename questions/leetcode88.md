---
title: Leetcode-88-Merge Sorted Array 
date: 2016-08-17 19:05:15
categories: 
- Code
tags:
- Leetcode

---
## Describe:
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.
## Solution:
给定两个有序整数数组nums1,nums2，把他们两个合并到nums1数组中

这题很简单，从后向前赋值就可以了

## Code:
```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int k,i,j;
        k=m+n-1;
        i=m-1;
        j=n-1;
        
        while(j>-1&&i>-1){
            nums1[k--] = nums1[i]>nums2[j]?nums1[i--]:nums2[j--];
        }
        if (i==-1){
            while(k>-1){
                nums1[k--]=nums2[j--];            
            }   
        }
        
    }
```