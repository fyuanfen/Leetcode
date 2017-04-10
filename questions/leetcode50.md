---
title: Leetcode-50-Pow(x, n)
date: 2017-04-09 23:53:52
categories: 
- Code
tags:
- Leetcode


---

题目描述
给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

## Solution

这题看似简单实则暗藏深坑，要注意以下几点
异常值和大指数问题

1. 全面考察指数的正负、底数是否为零等情况。

2. 写出指数的二进制表达，例如13表达为二进制1101。

3. 举例:`10^1101 = 10^0001*10^0100*10^1000`。

4. 通过&1和>>1来逐位读取1101，为1时将该位代表的乘数累乘到最终结果。
 
 
```javascript
function Power(base, n) {
    var res = 1,curr = base;
    var exponent;
    if(n>0){
        exponent = n;
    }else if(n<0){
        if(base==0)
           return null;//分母不能为0
        exponent = -n;
    }else{// n==0
        return 1;// 0的0次方
    }
    while(exponent!=0){
        if((exponent&1)==1)
            res*=curr;
        curr*=curr;// 翻倍
        exponent>>=1;// 右移一位
    }
    return n>=0?res:(1/res);       
}
```\