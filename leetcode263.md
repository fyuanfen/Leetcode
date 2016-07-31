title: Leetcode-263-Ugly Number
date: 2016-07-30 12:30:53

categories: 
- Code
tags:
- Leetcode

---


# Ugly Number 

## Describe:

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.


## 解题思路：

这题很简单啦，判断一个正整数的质因子是不是仅为为2,3,5，可以用递归和迭代求解。


## 代码：
 

```java
public boolean isUgly(int num) {
    if(num==1) return true;
    if(num==0) return false;
	while(num%2==0) num=num>>1;
	while(num%3==0) num=num/3;
	while(num%5==0) num=num/5;
    return num==1;
}
```


该题进阶版[**Ugly NumberII**](http://zyy1314.com/2016/07/30/leetcode264/)，进一步获得第n个丑数。