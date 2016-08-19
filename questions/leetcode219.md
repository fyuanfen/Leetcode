---
title: leetcode-219-Contains Duplicate II
date: 2016-08-18 11:23:09
categories: 
- Code
tags:
- Leetcode


---
# Contains Duplicate II
## Describe:


Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

传送门:
[**Contains Duplicate**](http://zyy1314.com/2016/08/18/leetcode217/)
[**Contains Duplicate II**](http://zyy1314.com/2016/08/18/leetcode219/)
[**Contains Duplicate III**](http://zyy1314.com/2016/08/18/leetcode220/)

## Solution:
给定一个整型数组，判断在相邻距离为k的元素中是否有重复数值

解题思路很简单：

1. 首先建立一个Set，依次加入k个数组元素，如果无法加入则说明有重复值

2. 加入数组的下一个元素，同时去掉set的第一个元素，直到数组的末尾



## Code:
```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
		  Set s= new HashSet<Integer>();
		  for(int i=0;i<nums.length;i++){
			  if (i>k)   s.remove(nums[i-k-1]);
			  if (!s.add(nums[i]))  return true;
		  }
	        return false;
	    }
```	  