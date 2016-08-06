
#  Reverse Vowels of a String
## Describe: 

Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".

Note:
The vowels does not include the letter "y". 
## Solution:

反转字符串中的元音字母a,e,i,o,u
这里很简单啦，java里面只需要用一个HashSet存储元音字母，然后遍历字符串，找到首尾的元音字母进行交换，实现代码如下：

## Code1:
```java
public class Solution {
    public String reverseVowels(String s) {
        char[] list=s.toCharArray();
       Set<Character> vowels = new HashSet<>(Arrays.asList(new Character[]{'a','e','i','o','u','A','E','I','O','U'}));
        for(int i=0,j=list.length-1;i<j;){
            if(!set.contains(list[i])){
                i++;
                continue;
            }
            if(!set.contains(list[j])){
                j--;
                continue;
            }
            char temp=list[i];
            list[i]=list[j];
            list[j]=temp;
            i++;
            j--;
        }
        return String.valueOf(list);
    }
}
```

当然，也可以用python来写，更简洁一些
## Code2:

``` python

def reverseVowels(self, s):
        vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'}
        L = list(s)
        i = 0
        j = len(L) - 1
        while i < j:
            while i < j and L[i] not in vowels:
                i += 1
            while j > i and L[j] not in vowels:
                j -= 1
            L[i], L[j] = L[j], L[i] 
            i += 1
            j -= 1
        return ''.join(L)
        

```