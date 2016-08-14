---
title: Leetcode-326-Power of Three
date: 2016-08-12 11:01:01
categories: 
- Code
tags:
- Leetcode

---



# Power of Three

# Describe:
Given an integer, write a function to determine if it is a power of three.

Follow up:
**Could you do it without using any loop / recursion?**
## Solution:
这题很简单，通过递归和迭代都可以很容易实现。



## Method1
很简单的方法，适用于求任何数的n次方，但执行效率较低。本题中可以把整数转为3进制，然后按照“10”匹配。

**这里使用`Integer.toString(data,n)`方法，可以把data转为n进制**
### Code1:
```java
public class Solution {
	public boolean isPowerOfThree(int n) {
    	return Integer.toString(n,3).matches("10*");//转为3进制

```



## Method2
还有个小trick的代码,用3的19次方对n取余数,余数为0即结果
### Code2:
```java
public class Solution {
	public boolean isPowerOfThree(int n) {
    	// 1162261467 is 3^19,  3^20 is bigger than int  
    	return ( n>0 &&  1162261467%n==0);
	}
}
```

## Method3


If log10(n) / log10(3) returns an int (more precisely, a double but has 0 after decimal point), then n is a power of 3. (original post). But be careful here, **you cannot use log (natural log) here, because it will generate round off error for n=243.** 

This is more like a coincidence.I mean when n=243, we have the following results:

>log(243) = 5.493061443340548    log(3) = 1.0986122886681098 ==> log(243)/log(3) = 4.999999999999999                           
>log10(243) = 2.385606273598312   log10(3) = 0.47712125471966244 ==> log10(243)/log10(3) = 5.0
   
  
This happens because log(3) is actually slightly larger than its true value due to round off, which makes the ratio smaller.

## Code3:
```java
public boolean isPowerOfThree(int n) {
    return (Math.log10(n) / Math.log10(3)) % 1 == 0;
}
```
