
---
title: Leetcode-151-Reverse Words in a String
date: 2016-08-02 14:27:19
categories: 
- Code
tags:
- Leetcode

---

# Reverse Words in a String

## Describe: 
Given an input string, reverse the string word by word.

For example,
Given s = "the sky is blue",
return "blue is sky the". 


## Solution1:
翻转字符串中的单词，这题常规解法是按照空格切分，再翻转，用python很容易写。

## Code:
```python
def reverseWords(self,s):
        s=s.strip()
        s=s.split(' ')[::-1]
        s=' '.join(i for i in s if i != '')
        return s


```

## Solution2:

It has another way to solve. The idea is to ignore the extra spaces, reverse words one by one and reverse the whole string in the end.
I think for the interview it is good to show that substr or istringstream can be used too.

[The idea is taken from here](http://www.ardendertat.com/2011/10/31/programming-interview-questions-12-reverse-words-in-a-string/)

## Code:
```cpp
class Solution {
public:

    // function to reverse any part of string from i to j (just one word or entire string)
    void reverseword(string &s, int i, int j){
        while(i<j){
          char t=s[i];
          s[i++]=s[j];
          s[j--]=t;
        } 
    }
    
    void reverseWords(string &s) {
        
        int i=0, j=0;
        int l=0;
        int len=s.length();
        int wordcount=0;
        
        while(true){
            while(i<len && s[i] == ' ') i++;  // skip spaces in front of the word
            if(i==len) break;
            if(wordcount) s[j++]=' ';
            l=j;
            while(i<len && s[i] != ' ') {s[j]=s[i]; j++; i++;} 
            reverseword(s,l,j-1);                // reverse word in place
            wordcount++;
            
        }
        
        s.resize(j);                           // resize result string
        reverseword(s,0,j-1);                  // reverse whole string
    }
};
```
