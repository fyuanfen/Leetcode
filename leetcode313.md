
# Super Ugly Number

## Describe:

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, [1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32] is the sequence of the first 12 super ugly numbers given primes = [2, 7, 13, 19] of size 4.

Note:
(1) 1 is a super ugly number for any given primes.
(2) The given numbers in primes are in ascending order.
(3) 0 < k ≤ 100, 0 < n ≤ 106, 0 < primes[i] < 1000.


## 解题思路：
这道题其实是LeetCode另外一道题[**Ugly Number II**](http://zyy1314.com/2016/07/30/leetcode264/)的general情况。思路是一样的，首先我们考虑一系列的数字是根据什么原则产生的。很显然，除了第一个数字，其余所有数字都是之前已有数字乘以任意一个在质数数组里的质数.

所以对于每一个已有的数字，我们都可以分别乘以所有在质数数组里的质数得到一系列的数字，这些数字肯定会存在在以后的序列中。由于我们是要得到从小到大的结果，所以我们可以维护个count数组，来记录对于对应质数下一个需要被乘的已有数的index, 我们取最小的结果当做下个数，对于那个最小的结果，需要增加count数组中那个质数对应的index,表明下一次用下个已有的数来乘对应的质数。

有些tricky的地方是对于已有序列中的数，乘不同质数得到的结果会可能存在重复，比如题目中例子2, 7与7, 2就重复了，解决方法很简单，就是只要是等于最小的结果，就增加对应count数组中的元素，具体见代码。


## 代码：


```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] count = new int[primes.length];
        int[] res = new int[n];
        res[0] = 1;

        for (int i = 1; i < n; i++) {
            int min = Integer.MAX_VALUE;
            
            // 找出候选数字的最小值
            for (int j = 0; j < primes.length; j++) {
                min = Math.min(min, primes[j] * res[count[j]]);
            }
            res[i] = min;
            
            // 增加与最终结果对应的质数的元素
            for (int j = 0; j < count.length; j++) {
                // 所有符合条件的，都需增加对应prime index, 避免重复
                if (res[count[j]] * primes[j] == min) {
                    count[j]++;
                }
            }
        }
        return res[n - 1];
    }
}


```



