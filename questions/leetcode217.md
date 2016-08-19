---
title: leetcode217-Contains Duplicate
date: 2016-08-18 11:21:07
categories: 
- Code
tags:
- Leetcode

---
# Contains Duplicate
## Describe:
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.


传送门:

[**Contains Duplicate**](http://zyy1314.com/2016/08/18/leetcode217/)
[**Contains Duplicate II**](http://zyy1314.com/2016/08/18/leetcode219/)
[**Contains Duplicate III**](http://zyy1314.com/2016/08/18/leetcode220/)


## Solution:
使用set保存数组元素,
ps：题外话，这个代码很简单的，但是提交了N次，每次都有新体验，有时候AC，有时候超时。

所以忠告就是，多try几次吧，try try 总有可能过得
## Code:

```java
 public boolean containsDuplicate(int[] nums) {
         Set<Integer> set = new HashSet<Integer>();
		 for(int i : nums){
			 if(!set.add(i))// if there is same
				 return true; 
		 }
		 return false;
    }
```  
    另外，我python大法就是好，一行搞定,哦呵呵呵
    
```python    
def containsDuplicate(self, nums):
    return len(nums) != len(set(nums))
```