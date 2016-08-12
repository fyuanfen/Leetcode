---
title: Leetcode-20-Valid Parentheses
date: 2016-08-02 08:38:00
categories: 
- Code
tags:
- Leetcode

---

# Valid Parentheses

## Describe:
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

Subscribe to see which companies asked this question

## Soloution:
这道题目考察的是非常基本的堆栈操作。验证括号是否匹配，该题还有进阶版本[**Generate Parentheses**](http://zyy1314.com/2016/08/02/leetcode22/)

从头到尾扫描字符串，switch语句当前字符如果为"(,{,["则入栈。

如果当前字符和栈顶的字符匹配，则执行出栈pop操作，继续循环；
如果不匹配，则返回false。



## Code :
```java
	public boolean isValid(String s) {
	    Stack<Character> stack = new Stack<>();
	    for (int i = 0; i < s.length(); i++) {
	        switch (s.charAt(i)) {
	            case '(':
	                stack.push('(');
	                break;
	            case '{':
	                stack.push('{');
	                break;
	            case '[':
	                stack.push('[');
	                break;
	            case ')':
	                if (stack.size() == 0 || stack.pop() != '(')
	                    return false;
	                break;
	            case '}':
	                if (stack.size() == 0 || stack.pop() != '{')
	                    return false;
	                break;
	            case ']':
	                if (stack.size() == 0 || stack.pop() != '[')
	                    return false;
	                break;
	        }
	    }
	    return stack.isEmpty();
	}
		  
	     

```

