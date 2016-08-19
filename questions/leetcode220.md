---
title: Leetcode-220-Contains Duplicate III
date: 2016-08-18 11:29:41
categories: 
- Code
tags:
- Leetcode

---


# Contains Duplicate III
## Describe:
Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] and nums[j] is at most t and the difference between i and j is at most k.

给定一个数组，确定数组是否有这样两个元素。数组元素下标相隔不超过k，元素大小相差不超过t

传送门:

[**Contains Duplicate**](http://zyy1314.com/2016/08/18/leetcode217/)
[**Contains Duplicate II**](http://zyy1314.com/2016/08/18/leetcode219/)
[**Contains Duplicate III**](http://zyy1314.com/2016/08/18/leetcode220/)

---

这题有两种解法：
## Solution1:滑动窗口 + TreeSet

**TreeSet数据结构（Java）使用红黑树实现，是平衡二叉树的一种。**

该数据结构支持如下操作：

1. floor()方法返set中小于等于给定元素的最大元素；如果不存在这样的元素，则返回 null。

2. ceiling()方法返回set中大于等于给定元素的最小元素；如果不存在这样的元素，则返回 null。


## Code1:
```java
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if(k < 1 || t < 0)
            return false;
        TreeSet<Integer> set = new TreeSet<Integer>();
        for(int i = 0; i < nums.length; i++){
            int n = nums[i];
            if(set.floor(n) != null && n <= t + set.floor(n) || 
                    set.ceiling(n) != null && set.ceiling(n) <= t + n)
                return true;
            set.add(n);
            if (i >= k)
                set.remove(nums[i - k]);
        }
        return false;
    }
 ```
 
 ---
 
## Solution2:Bucket排序
第二种方法是使用桶排序算法

假定把数组元素分到多个桶中，这里桶需要设置为合理的大小。使得相差t的元素一定会映射到同一个桶或者相邻的桶中。

例如，桶的大小是3，这样0，1，2就映射到同一个桶中。
当t=3时，0和3被视作重复元素，但他们处于相邻的桶中。


因此，我们需要**设置合理的桶的大小
**，通常设置为t或者t+1。这里我们设置为t+1，以避免考虑t=0的情况。(**注意：t=0时，该问题退化为[Contains Duplicate II]()**)这样每个元素就被映射到第n/(t+1)个桶中。

这样，判断两个元素大小相差t的话，我们仅需要考虑以下两种情况：

1. 这两个元素是否在同一个桶中
2. 这两个元素是否在相邻桶中，且大小相差小于等于t


## Code2:

```python
def containsNearbyAlmostDuplicate(self, nums, k, t):
    if t < 0: return False
    n = len(nums)
    d = {}
    w = t+1
    for i in xrange(n):
        m = nums[i] / w
        if m in d:
            return True
        if m - 1 in d and abs(nums[i] - d[m - 1]) < w:
            return True
        if m + 1 in d and abs(nums[i] - d[m + 1]) < w:
            return True
        d[m] = nums[i]
        if i >= k: 
        	del d[nums[i - k] /w]
    return False
```


更简短一些，我们可以写成:

```python
def containsNearbyAlmostDuplicate(self, nums, k, t):
        if k <= 0 or t < 0:
            return False
        numsDict = {}
        for i in range(len(nums)):
            bucket = nums[i]/(t+1)
            for key in [bucket-1, bucket, bucket+1]:
                if key in numsDict and abs(numsDict[key] - nums[i]) <= t:
                    return True
            numsDict[bucket] = nums[i]
            if i+1 > k:
                pop_key = nums[i-k]/(t+1)
                numsDict.pop(pop_key)
        return False
        
        
```

还有一个难点就是，在整数数组里可能有负数。这样**在java（C和C++）中，num/t+1会使得[-t-1,0]的所有的数都映射到0号桶**。（ps:python则不会,具体参考[**python负数除法**](http://zyy1314.com/2016/08/19/python%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B04-%E8%B4%9F%E6%95%B0%E9%99%A4%E6%B3%95%E5%92%8C%E5%8F%96%E6%A8%A1%E8%BF%90%E7%AE%97/) )

eg:
-t-1,-t...-1属于-1号桶

0,1,2...t属于0号桶


但是使用`nums[i]/t+1`这个公式会使得-1号桶的元素映射到0号桶中

对此我们有两种解决方案：

1. **将每一个数组元素的起点调整为Integer.MIN_VALUE**,即每个元素改为num-Integer.MIN_VALUE,桶号都为正数

2. **将正数元素映射到num/t+1号桶，负数元素映射到(num+1)/(t+1)-1号桶**

此外，因为增加了元素的大小，这里考虑到java的Int会溢出，计算时需要使用Long类型（python不会溢出）


Java代码：
```java
 public class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k < 1 || t < 0) return false;
        Map<Long, Long> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            long remappedNum = (long) nums[i] - Integer.MIN_VALUE;
            long bucket = remappedNum / ((long) t + 1);
            if (map.containsKey(bucket)
                    || (map.containsKey(bucket - 1) && remappedNum - map.get(bucket - 1) <= t)
                        || (map.containsKey(bucket + 1) && map.get(bucket + 1) - remappedNum <= t))
                            return true;
            if (i >= k) {
                long lastBucket = ((long) nums[i - k] - Integer.MIN_VALUE) / ((long) t + 1);
                map.remove(lastBucket);
            }
            map.put(bucket, remappedNum);
        }
        return false;
    }
}

```

```java
private long getID(long i, long w) {
    return i < 0 ? (i + 1) / w - 1 : i / w;
}

public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    if (t < 0) return false;
    Map<Long, Long> d = new HashMap<>();
    long w = (long)t + 1;
    for (int i = 0; i < nums.length; ++i) {
        long m = getID(nums[i], w);
        if (d.containsKey(m))
            return true;
        if (d.containsKey(m - 1) && Math.abs(nums[i] - d.get(m - 1)) < w)
            return true;
        if (d.containsKey(m + 1) && Math.abs(nums[i] - d.get(m + 1)) < w)
            return true;
        d.put(m, (long)nums[i]);
        if (i >= k) d.remove(getID(nums[i - k], w));
    }
    return false;
}
```
