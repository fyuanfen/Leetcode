---
title: Leetcode-191-Number of 1 Bits 
date: 2016-08-13 08:20:33
categories: 
- Code
tags:
- Leetcode

---
# Number of 1 Bits 
## Describe:
Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation `00000000000000000000000000001011`, so the function should return 3.

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

## Solution:

Java中的位运算符：

`>>`表示右移，如果该数为正，则高位补0，若为负数，则高位补1；

`>>>`表示无符号右移，也叫逻辑右移，即若该数为正，则高位补0，而若该数为负数，则右移后高位同样补0。
这里要使用`>>>`，因为当输入的数为一个负数的时候，比如0x8000-0000，当右移一位变成0x0400-0000，其实不是这样的，因为移位前是一个负数，所以我们要保证移位后的数也是一个负数，因此移位后改数变为0xC000-0000.最高位永远都是1，最终这个数字会变成0xFFFF-FFFF，程序陷入死循环。


统计一个数字的二进制格式的1的数目
可参考[**Reverse Bits**](http://zyy1217.com/2016/08/13/leetcode190/)

[**Counting Bits**](http://zyy1217.com/2016/08/13/leetcode338/)统计小于n的每个数字二进制格式中的1的个数

## Code:
```java
    public int hammingWeight(int n) {
        int result=0;
        while(n!= 0){
            result = result + (n&1);
            n = n>>>1;
        }
        return result;
    }
```

### 解法2：
判断二进制数某一位的情况可以利用与某个掩码的与来判断，初始时掩码 mask=0x01，然后逐次将mask左移一位

```javascript
function NumberOf1(n) {   
    var i = 1;
    	count = 0;
    while(i) {
    	if(n & i) {
    		count ++;
        }
    	i = i << 1;   
    }
   	return count;
}
```

### 解法4：

如果一个整数不为0，那么这个整数至少有一位是1。如果我们把这个整数减1，那么原来处在整数最右边的1就会变为0，原来在1后面的所有的0都会变成1(如果最右边的1后面还有0的话)。其余所有位将不会受到影响。
举个例子：一个二进制数1100，从右边数起第三位是处于最右边的一个1。减去1后，第三位变成0，它后面的两位0变成了1，而前面的1保持不变，因此得到的结果是1011.我们发现减1的结果是把最右边的一个1开始的所有位都取反了。这个时候如果我们再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。如1100&1011=1000.也就是说，把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。

```javascript
function NumberOf1(n)
{
    var count = 0;
    while(n) {
        n = n&(n-1);
        count++;
    }
    return count;
}
```