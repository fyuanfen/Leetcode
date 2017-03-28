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




title: Leetcode-264-Ugly NumberII
date: 2016-07-30 12:30:53

categories: 
- Code
tags:
- Leetcode
- Dynamic Programming

---


# Ugly Number II

## Describe:

Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number.


<!-- more --> 

## 解题思路：

第二题在第一题[**Ugly Number**](http://zyy1217.com/2016/07/30/leetcode263/)的基础上，进一步让我们获得第n个丑数。

根据上述思路可以做如下实现：

丑数序列是 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, …
我们可以发现下一个丑数都是之前的丑数乘以2，3或者5。因此我们只需要用indexn记录下当前因子n出现的次数。

假定丑数序列为u[n],则对于每个质因子，我们有以下序列：

(1) u[0]×2, u[1]×2,  u[2]×2,  u[3]×2,  u[4]×2,  u[5]×2, …

(2) u[0]×3, u[1]×3,  u[2]×3,  u[3]×3,  u[4]×3,  u[5]×3, …

(3) u[0]×5, u[1]×5,  u[2]×5,  u[3]×5,  u[4]×5,  u[5]×5, …


![](http://images.zyy1217.com/QQ20170328-0.jpg)


  相当于对以上的三个丑数序列进行排序和去重，只不过要注意，u[2]依赖于u[1]，u[1]依赖于u[0]，因此需要从u[0]开始计算。其中u[0]初始化为1，
 
### 第一遍计算：
 
 min(u[0]×2,u[0]×3,u[0]×5),获得最小值u[1] = u[0]*2 =2,队列变成
 
 
(1) <del> u[0]×2 </del>, u[1]×2,  u[2]×2,  u[3]×2,  u[4]×2,  u[5]×2, …

(2) u[0]×3, u[1]×3,  u[2]×3,  u[3]×3,  u[4]×3,  u[5]×3, …

(3) u[0]×5, u[1]×5,  u[2]×5,  u[3]×5,  u[4]×5,  u[5]×5, …

### 第二遍计算：
 
 min(u[1]×2,u[0]×3,u[0]×5),获得最小值u[2] = u[0]*3 =3,队列变成
 
  
(1) <del> u[0]×2 </del>, u[1]×2,  u[2]×2,  u[3]×2,  u[4]×2,  u[5]×2, …

(2) <del> u[0]×3 </del>, u[1]×3,  u[2]×3,  u[3]×3,  u[4]×3,  u[5]×3, …

(3) u[0]×5, u[1]×5,  u[2]×5,  u[3]×5,  u[4]×5,  u[5]×5, …


### 第三遍计算：
 
 min(u[1]×2,u[1]×3,u[0]×5),获得最小值u[3] = u[1]*2 =4,队列变成
 
  
(1) <del> u[0]×2 </del>, <del>u[1]×2</del>,  u[2]×2,  u[3]×2,  u[4]×2,  u[5]×2, …

(2) <del> u[0]×3 </del>, u[1]×3,  u[2]×3,  u[3]×3,  u[4]×3,  u[5]×3, …

(3) u[0]×5, u[1]×5,  u[2]×5,  u[3]×5,  u[4]×5,  u[5]×5, …


我们可以发现下一个丑数都是当前丑数乘以2，3或者5。因此我们只需要用indexn记录下当前因子n出现的次数。

要注意的是，会出现下一个丑数同时满足多个条件。如6满足 2 X 3 ，也满足3 X 2，此时对应的都要更新，不能只更新第一个，所以代码中用的是**三个if，而不能是if,  else if**



注意：本题是求质因子为2,3,5的ugly nuber，求k个质因子的ugly number,详见[**Super Ugly Number**](http://zyy1217.com/2016/07/30/leetcode313/)

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