---
title: Leetcode-70-Climbing Stairs
date: 2016-09-11 10:53:52
categories: 
- Code
tags:
- Leetcode
- Dynamic Programming

---



# Climbing Stairs
## Describe:
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
## Solution:

本题对应了《剑指offer》上的跳台阶。 
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。


本题是一道很典型的递归题目，根据题目的初始条件可知：

```
f(1) = 1;
f(2) = 2;
f(n) = f(n-1) + f(n-2) （n > 2）
```
对于n个台阶时的解释是，最后青蛙可以一次跳一个台阶，则解法是f(n-1)；也可以直接跳两个台阶，则解法是f(n-2)。

其实到这里大家可以发现本题和斐波拉切数列的思路相同，不同点仅仅在于初始条件，因此可以使用递归得到结果。然而本题的递归过程中会涉及到太多的重复计算。因为在计算f(n)的时候需要计算f(n-1)和f(n-2)，而在计算f(n-1)时本身也是需要计算f(n-2)的。所以还是不采用递归的方式，使用两个变量分别表示为f(n-1)和f(n-2)并更新这两个变量，从而得到最终结果。



## Code:

```javascript
	
function jumpFloor(n)
{
    // write code here
    if (n<=0) return 0;
    if (n<=2) return n;

    var minusOne = 2,
        minusTwo = 1,
        fib;
    for(var i = 2; i < n;i++) {
        fib = minusOne + minusTwo;
        minusTwo = minusOne;
        minusOne = fib;   
    }
    
    return fib;
}  
```
    
    
# 变态跳台阶

本题是在上一题的基础上的升级版，来源于《剑指offer》。

## 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

## 解题思路
当有n个台阶时,分析如下: 

```
f(1) = 1 
f(2) = f(2-1) + f(2-2) //f(2-2) 表示2阶一次跳2阶的次数。 
f(3) = f(3-1) + f(3-2) + f(3-3) 
… 
f(n) = f(n-1) + f(n-2) + f(n-3) + … + f(n-(n-1)) + f(n-n)
```
这里的f(n) 代表的是n个台阶有一次1,2,…n阶的 跳法数。
n = 1时，只有1种跳法，f(1) = 1
n = 2时，会有两个跳得方式，一次1阶或者2阶，这回归到了问题（1） ，f(2) = f(2-1) + f(2-2)

n = n时，会有n种跳的方式，1阶、2阶…n阶，得出结论：

```
f(n) = f(n-1)+f(n-2)+…+f(n-(n-1)) + f(n-n) => f(0) + f(1) + f(2) + f(3) + … + f(n-1)
```

因此我们按照这个思路，我们可以写出以下代码

```javascript
function jumpFloorII(n)
{
    var d = [1,1];//d[0] =0,d[1]=1
    var tmp;
    if(n < 2) {return d[n];}
    for( var j = 2;j <= n; j++) {//一共多少台阶
        tmp = 0;
       for(var i = 1;i <= j; i++) {//一次跳几个台阶
          tmp += d[j-i];
       }
        d[j] =tmp;
   }
    return d[n];
      

}
```


以上已经是一种结论，但是为了简单，我们可以继续简化：

```
f(n-1) = f(0) + f(1)+f(2)+f(3) + … + f((n-1)-1) = f(0) + f(1) + f(2) + f(3) + … + f(n-2)
f(n) = f(0) + f(1) + f(2) + f(3) + … + f(n-2) + f(n-1) = f(n-1) + f(n-1)
```
可以得出： 

```
f(n) = 2*f(n-1)
```
得出最终结论,在n阶台阶，一次有1、2、…n阶的跳的方式时，总得跳法为f(n)：

```
1 ,(n=0 )
1 ,(n=1 )
2*f(n-1),(n>=2)
```
代码如下：

```java
public class Solution {
    public int JumpFloorII(int target) {
        if (target <= 0) {
            return -1;
        } else if (target == 1) {
            return 1;
        } else {
            return 2 * JumpFloorII(target - 1);
        }
    }
}
```

更简单一点，可以吧上式规约为`2^(n-1)`：

将1左移动n-1次

```java
public class Solution {
    public int JumpFloorII(int target) {
        return  1<<--number;
    }
}
```