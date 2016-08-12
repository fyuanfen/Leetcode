---
title: 	Leetcode-383-Ransom Note
date: 2016-08-12 14:45:58

categories: 
- Code
tags:
- Leetcode

---

# Ransom Note

## Describe:
Given an arbitrary ransom note string and another string containing letters from all the magazines,write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false. 

Each letter in the magazine string can only be used once in your ransom note. 

Note:
You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

## Solution:

判断一个字符串是否能由第二个串构造
思想很简单，首先建立一个长度为26的数组，存储magazine的每个字母出现的次数
然后遍历ransomnote，每遍历一次该字母数目递减


本题同系列题目[**Valid Anagram**](http://zyy1314.com/2016/08/12/leetcode242/)是判断两个字符串组成元素是否相同
## Code:

```java
 public boolean canConstruct(String ransomNote, String magazine) {
    	int[] arr = new int[26];
    	for (int i=0;i<magazine.length();i++){
    		arr[magazine.charAt(i)-'a']++;	
    	}
    	for (int i=0;i<ransomNote.length();i++){
    		
    		if (--arr[ransomNote.charAt(i)-'a']<0)
    			return false;
    		
    	}
        
    	return true;
```