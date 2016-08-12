---
title: Leetcode-242-Valid Anagram
date: 2016-08-11 20:13:20

categories: 
- Code
tags:
- Leetcode

---

# Valid Anagram

## Describe:
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solution:
就是判断给定的两个字符串是不是由同样的字母组成

本题同系列题目[**Ransom Note**](http://zyy1314.com/2016/08/12/leetcode383/)是判断一个字符串是否由另一个字符串的元素组成

## Code:

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] alphabet = new int[26];
        for (int i = 0; i < s.length(); i++) alphabet[s.charAt(i) - 'a']++;
        for (int i = 0; i < t.length(); i++) alphabet[t.charAt(i) - 'a']--;
        for (int i : alphabet) if (i != 0) return false;
        return true;
    }
}
```

同样的，也可以利用字典解决
```python
def isAnagram1(self, s, t):
    dic1, dic2 = {}, {}
    for item in s:
        dic1[item] = dic1.get(item, 0) + 1
    for item in t:
        dic2[item] = dic2.get(item, 0) + 1
    return dic1 == dic2
```
    
    
或者利用python的排序函数，然后判断两个子串是否相同    
```python     
def isAnagram3(self, s, t):
    return sorted(s) == sorted(t)
    
```



或者统计两个子串元素的个数
```python
def isAnagram(self, s, t):
        if set(s) != set(t):
            return False
        else:
            for element in set(s):
                if s.count(element) != t.count(element):
                    return False
            return True
```