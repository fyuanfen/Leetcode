

# Sum of Two Integers

## Describe: 
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:
Given a = 1 and b = 2, return 3.

两个数相加，但不能使用“+”,"-" 操作符。

## Solution:


首先想到不能使用加减操作符，然后想到按位模拟运算。
先看异或运算：  0 ^ 0 = 0    0 ^ 1 = 1   1 ^ 0 = 1   1 ^ 1 = 0
再看加法的进位运算：  0 + 0 = 1    0 + 1 = 1   1 + 0 = 1    1 + 1 = 0(进位)


异或运算与加法运算除了进位的话结果完全一样，所以如果没有进位的话，我们可以直接用异或替代加法。

再考虑进位运算， 只有当 两位都是1 时才会进位，那么通过与运算& 我们就可以得到所有两个数都为1 的位，由于进位是要加到高位上的，所以我们再把与之后的结果左移一位，与异或后的结果相加，就可以得到完整的加法结果。
具体步骤如下： 
1、输入 a，b 
2、按照位把ab相加，不考虑进位，结果是 a xor b，即1+1 =0 0+0 = 0 1+0=1，进位的请看下面 
3、计算ab的进位的话，只有二者同为1才进位，因此进位可以标示为 (a and b) << 1 ，注意因为是进位，所以需要向左移动1位 
4、于是a+b可以看成 （a xor b）+ （(a and b) << 1），这时候如果 (a and b) << 1 不为0，就递归调用这个方式吧，因为（a xor b）+ （(a and b) << 1） 也有可能进位，所以我们需要不断的处理进位。

## Code:

```java
public class Solution {
    public int getSum(int a, int b) {
        int result = a ^ b; // 按位加
        int carray = (a & b) << 1; // 计算进位
        if(carray!=0) 
        	return  getSum(result,carray); //判断进位与处理
        return result;
    }
}
```