---
title: Leetcode-226-Invert Binary Tree
date: 2016-08-12 13:45:59
categories: 
- Code
tags:
- Leetcode
---


# Invert Binary Tree
## Describe:
![](http://oavk3bisu.bkt.clouddn.com/invert_tree.png)

>Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so fuck off.
## Solution:
题目很简单，就是反转二叉树

可是我快要被上面google的哏儿笑死了，2333333333333333

程序猿真是呆萌可爱O(∩_∩)O


## Code:
```java
public TreeNode invertTree(TreeNode root) {
        if (root==null)
            return null;
            TreeNode tmp=root.left;
    
            root.left = invertTree(root.right);
            root.right = invertTree(tmp);
            return root;
        }
        
        
 ```

 --uppdate--
 时隔半年，二刷了。这次用js，所以要考虑到空类型问题，加个判空的函数


 ```javascript
 function TreeNode(x) {
     this.val = x;
     this.left = null;
     this.right = null;
 }
 function isEmpty(item){
     for(var i in item){
         return false;
     }
     return true;

 }
 function Mirror(root)
 {
     // write code here
     if(isEmpty(root)) return root;
     var temp = root.left;
     root.left = root.right;
     root.right= temp;
     Mirror(root.right);
     Mirror(root.left);

 }

 ```