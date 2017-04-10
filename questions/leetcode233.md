---
title: Leetcode-233-Number of Digit One
date: 2017-04-03 18:12:24
categories: 
- Code
tags:
- Leetcode

---
# Number of Digit One
Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

For example: 
Given n = 13, 
Return 6, because digit 1 occurred in the following numbers: 1, 10, 11, 12, 13.


## 题目理解：

题目的意思是给定一个数n，计算[0, n]的区间中1出现的次数。

## 具体思路：

对这个数字的每一位求存在1的数字的个数。从个位开始到最高位。

举个例子54215，比如现在求百位上的1，54215的百位上是2。可以看到xx100到xx199的百位上都是1，这里xx从0到54，即100->199, 1100->1199...54100->54199, 这些数的百位都是1，因此百位上的1总数是`55*100`。

如果n是54125,这时由于它的百位是1，先看xx100到xx199，其中xx是0到53，即`54*100`, 然后看54100到54125，这是26个。所以百位上的1的总数是`54*100 + 26`.

如果n是54025，那么只需要看xx100到xx199中百位上的1，这里xx从0到53，总数为`54*100`

求其他位的1的个数的方法是一样的。



## 总结规律

其实通过上面的分析，我们就可以归纳出一个规律如下。

要求第i位1出现的次数，并且i的高位数为highN，低位数为lowN，当前第i位的数字为cdigit，则当前i位1出现的次数分三种情况：

```
cdigit == 0, count = highN * factor.
cdigit == 1, count = highN * factor + lowN + 1.
cdigit > 1, count = (highN + 1) * factor.
```
其中，factor为当前的乘积因子，例如百位的factor为100，十位的乘积因子为10。

有了规律，代码只要按照规律写出来即可。

```java

public class NumberofDigitOne {
    public int countDigitOne(int n) {
        int count = 0;
        long factor = 1;
        long cdigit = 0;
        long highN = 0;
        int lowN = 0;

        while (n / factor > 0) {
            cdigit = (n % (factor * 10)) / factor;
            highN = n / (factor * 10);

            if (cdigit == 0) {
                count += highN * factor;
            } else if (cdigit == 1) {
                count += highN * factor + lowN + 1;
            } else {
                count += (highN + 1) * factor;
            }

            lowN += cdigit * factor;
            factor *= 10;
        }


        return count;
    }

    public static void main(String[] args) {
        int n = 1410065408;
        NumberofDigitOne ndo = new NumberofDigitOne();
        int count = ndo.countDigitOne(n);

        System.out.println(count);
    }
}
```
