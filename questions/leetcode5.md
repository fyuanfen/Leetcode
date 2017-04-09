---
title: Leetcode-70-Longest Palindromic Substring
date: 2017-04-09 20:53:52
categories: 
- Code
tags:
- Leetcode
- Dynamic Programming

---

# Longest Palindromic Substring 最长回文串
 

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

 
同系列题目:

回文数字[**Palindrome Number**](http://zyy1217.com/2016/08/14/leetcode9/)

回文链表[**Palindrome Linked List**](http://zyy1217.com/2016/08/14/leetcode234/)

回文字符串[**Valid Palindrome**](http://zyy1217.com/2016/08/14/leetcode125/)


我们知道传统的验证回文串的方法就是两个两个的对称验证是否相等，那么对于找回文字串的问题，就要以每一个字符为中心，像两边扩散来寻找回文串，这个算法的时间复杂度是O(n*n)，可以通过OJ，就是要注意奇偶情况，由于回文串的长度可奇可偶，比如"bob"是奇数形式的回文，"noon"就是偶数形式的回文，两种形式的回文都要搜索，参见代码如下：

## 解法一：

```java
public class Solution {
private int lo, maxLen;

public String longestPalindrome(String s) {
	int len = s.length();
	if (len < 2)
		return s;
	
    for (int i = 0; i < len-1; i++) {
     	extendPalindrome(s, i, i);  //assume odd length, try to extend Palindrome as possible
     	extendPalindrome(s, i, i+1); //assume even length.
    }
    return s.substring(lo, lo + maxLen);
}

private void extendPalindrome(String s, int j, int k) {
	while (j >= 0 && k < s.length() && s.charAt(j) == s.charAt(k)) {
		j--;
		k++;
	}
	if (maxLen < k - j - 1) {
		lo = j + 1;
		maxLen = k - j - 1;
	}
}}
```

## 更好的解法二：
不过也可以通过另一种方法，不用考虑回文字符串的个数是奇数还是偶数。
原理是不管回文字符串的个数是奇数还是偶数，只需要以每一个字符为中心，先找到与该字符相同的最右边的位置，（这就是回文串中心的右边界），然后向两边扩散来寻找回文串。

eg：

```
adbcbda //长度为7

adbbda //长度为6
```

首先从s[i]开始，向右遍历，找到等于s[i]的最右的字符s[j]。再从s[i]，s[j]分别向两边扩展，判断s[i--],s[j++]是否相同。

代码如下：


```java
public String longestPalindrome(String s) {
    if (s.isEmpty()) return "";
    if (s.length() == 1) return s;
    int min_start = 0, max_len = 1;
    for (int i = 0; i < s.length(); ) {
        if (s.length() - i <= max_len / 2) break;
        int j = i, k = i;
        while (k < s.length() - 1 && s.charAt(k + 1) == s.charAt(k)) ++k; // Skip duplicate characters.
        i = k + 1;
        while (k < s.length() - 1 && j > 0 && s.charAt(k + 1) == s.charAt(j - 1)) {
            ++k;
            --j;
        } // Expand.
        int new_len = k - j + 1;
        if (new_len > max_len) {
            min_start = j;
            max_len = new_len;
        }
    }
    return s.substring(min_start, min_start + max_len);
}
```
这里要注意：当找到的回文串长度的1/2大于 s.length-i，就可以提前终止循环，因为这之后找到的回文串长度肯定小于max_length

## 解法三：
**但是这题虽然我用动态规划做出来了，可是时间复杂度很高，不太好。写在这里仅供参考，反正前两种方案已经蛮好的了**

此题还可以用动态规划Dynamic Programming来解，根Palindrome Partitioning II 拆分回文串之二的解法很类似，我们维护一个二维数组dp，其中dp[i][j]表示字符串区间[i, j]是否为回文串，当i = j时，只有一个字符，肯定是回文串，如果i = j + 1，说明是相邻字符，此时需要判断s[i]是否等于s[j]，如果i和j不相邻，即i - j >= 2时，除了判断s[i]和s[j]相等之外，dp[j + 1][i - 1]若为真，就是回文串，通过以上分析，可以写出递推式如下：

```
	dp[i, j] = 1                                  if i == j

             = s[i] == s[j]                       if j = i + 1

             = s[i] == s[j] && dp[i + 1][j - 1]   if j > i + 1 
```              

代码实现如下：

```java
    public static void longestPalindrome (String str) {
        int n = str.length(),left = 0,len=0;
        int dp[][] = new int[n][n];
        for(int i = 0;i < n; i++) {
            dp[i][i] = 1;
        }
        //第一遍搜索下标：00 11 22 33
        //第二遍搜索下标：01 12 23 34
        //第三遍搜索下标：02 13 24 35
        for(int j = 0;j < n; j++) {//j代表下标相隔的距离大小
            for(int i = 0 ;i + j < n; i++){ //j索引从i开始，因为要对len进行赋值
                if( str.charAt(i) == str.charAt(i+j) ){
                    if(j<2 || dp[i + 1][i + j - 1] == 1 ) {
                        dp[i][i+j] = 1;
                    }
                }
                if(dp[i][i+j] ==1 && len < j+1) {
                    len = j+1;
                    left = i;
                }
            }
        }
        System.out.println(str.substring(left, left + len));
    }
```

最后要来的就是大名鼎鼎的[马拉车算法Manacher's Algorithm](http://www.cnblogs.com/grandyang/p/4475985.html)，这个算法的神奇之处在于将时间复杂度提升到了O(n)这种逆天的地步，而算法本身也设计的很巧妙，很值得我们掌握，代码实现如下：

```cpp

class Solution {
public:
    string longestPalindrome(string s) {
        string t ="$#";
        for (int i = 0; i < s.size(); ++i) {
            t += s[i];
            t += '#';
        }
        int p[t.size()] = {0}, id = 0, mx = 0, resId = 0, resMx = 0;
        for (int i = 0; i < t.size(); ++i) {
            p[i] = mx > i ? min(p[2 * id - i], mx - i) : 1;
            while (t[i + p[i]] == t[i - p[i]]) ++p[i];
            if (mx < i + p[i]) {
                mx = i + p[i];
                id = i;
            }
            if (resMx < p[i]) {
                resMx = p[i];
                resId = i;
            }
        }
        return s.substr((resId - resMx) / 2, resMx - 1);
    }
};

```