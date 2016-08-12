title: Leetcode-264-Ugly NumberII
date: 2016-07-30 12:30:53

categories: 
- Code
tags:
- Leetcode

---


# Ugly Number II

## Describe:

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number.


<!-- more --> 

## 解题思路：

第二题在第一题[**Ugly Number**](http://zyy1314.com/2016/07/30/leetcode263/)的基础上，进一步让我们获得第n个丑数。

根据上述思路可以做如下实现：

找第N个丑数，从1开始遍历的方法复杂度太高，这里只需要考虑到从小到大的开始的每个丑数，都是他前面某个数的2或3或5倍，因此从已有的丑数1出发，分别乘以2、3、5，找出其中最小的一个，得到第二个丑数为2。
再找第三个丑数的时候，就要注意到，由于1乘以2已经出现了，因此下一次是2 X 2, 1 x 3, 1 X 5，后面的逻辑类似。要注意的是，会出现下一个丑数同时满足多个条件。如6满足 2 X 3 ，也满足3 X 2，此时对应的都要更新，不能只更新第一个，所以代码中用的是三个if，而不能是if,  else if

**具体流程如下：**
u[0]=1

u[1]=min(u[0] X 2,u[0] X 3,u[0] X 5)=2,	index[0]++

u[2]=min(u[1] X 2,u[0] X 3,u[0] X 5)=3,	index[1]++

u[3]=min(u[1] X 2,u[1] X 3,u[0] X 5)=5,	index[2]++

u[4]=min(u[1] X 2,u[1] X 3,u[1] X 5)=4,	index[0]++

u[5]=min(u[2] X 2,u[1] X 3,u[1] X 5)=6,	index[0]++,index[1]++

u[6]=min(u[3] X 2,u[2] X 3,u[1] X 5)=10,index[2]++


注意：本题是求质因子为2,3,5的ugly nuber，求k个质因子的ugly number,详见[**Super Ugly Number**](http://zyy1314.com/2016/07/30/leetcode313/)

## Code：
 

```java
 public int nthUglyNumber(int n) {
	    int[] u = new int[n];
	    u[0] = 1;
	    int index2 = 0, index3 = 0, index5 = 0;
	    
	    for (int i = 1; i < n; i++) {
	        // generate ugly number by multiply all the factors
	        u[i] = Math.min(u[index2] * 2, Math.min(u[index3] * 3, u[index5] * 5));
	        
	        // bump up index for the current minimum ugly number 
	        if (u[i] == u[index2] * 2) index2++;
	        if (u[i] == u[index3] * 3) index3++;
	        if (u[i] == u[index5] * 5) index5++;
	    }
	    
	    return u[n - 1];
	}
```