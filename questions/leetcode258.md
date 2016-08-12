title: Leetcode-258-Add Digits
date: 2016-08-01 09:14:38
categories: 
- Code
tags:
- Leetcode

---

# Add Digits

## Describe:
Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

<!-- more --> 

## Solution1:
Let's take a couple of example to check the input and expected output of the given problem.

### Example :
Input: 267
Step 1: 2+6+7 = 15
Step 2: 1+5 = 6 (Expected output as this number has single digit)


By looking at the above examples the first solution that comes to mind is that we can take the input number and find the sum of individual digits by using recursion (or iteration). If the result is not a single digit code we ill process the result again and keep doing it until it returns a single digits. 

### Code:

```java
public int addDigits(int num) {
while(num/10>0){
num = sumDigits(num);
}
return num;
}

public int sumDigits(int n){
    if(n==0)
        return 0;
    return (n%10) + sumDigits(n/10);
}
```
--- 

## Solution2:
From Wikipedia,you can find the conception[**Digital root**](https://en.wikipedia.org/wiki/Digital_root)


这是个求解十进制的数根问题，同样，我们可以把它引申到n进制问题，只需要把9换成n-1即可。

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>


The essence of this problem is that\\(10\equiv 1   (mod    9)\\), and thus \\(10^{k}\equiv 1^{k}\equiv 1    (mod    9)\\)

Concretely, for a three-digit number,
$$d(abc) \equiv a\times 10^{2} + b\times 10 + c \times 1 \equiv a\times 1 + b\times 1 + c \times 1   (mod    9)$$


Then I will give you an example to prove the conclusion:

**一个数余9等于这个数的数根余9。**

### Example: 
12345 ＝ 1 X 10000 ＋ 2 X 1000 ＋ 3 X 100 ＋ 4 x 10 ＋ 5

12345 ＝ 1 X（9999 ＋ 1） ＋ 2 X（999 ＋ 1） ＋ 3 X （99 ＋ 1） ＋ 4 x（9 ＋ 1） ＋ 5

12345 ＝ (1 X 9999 ＋ 2 X 999 ＋ 3 X 99 ＋ 4 X 9) ＋ （1 ＋ 2 ＋3 ＋ 4 ＋ 5）

12345 ％ 9 ＝ （1 ＋ 2 ＋ 3 ＋ 4 ＋ 5）％ 9


12345 ％ 9 ＝ （1 ＋ 2 ＋ 3 ＋ 4 ＋ 5）％ 9 ＝ 15 ％ 9 ＝ （1 ＋ 5）％ 9 ＝ 6 ％ 9


This process can be continued until a number less than 9 is gotten, i.e. num % 9. 

For any digit n, n = n % 9 unless n = 9. The only confusing case is n % 9 = 0, but addDigits(num) = 0 if and only if num = 0, otherwise it should be 9 in fact.


![image](http://oavk3bisu.bkt.clouddn.com/leetcode258.png)

### Code:

```java

public int addDigits(int num) {
if(num<10)
    return num;
else if(num%9 ==0)
    return 9;
else
    return num%9;        
}
```

We can step forward to get the conclusion:

$$d_{r}^{}= 1+((n-1)\mod 9)$$

### Code :
```java
public int addDigits(int num) {
     return (num-1)%9+1;
}
```
## Reference :
