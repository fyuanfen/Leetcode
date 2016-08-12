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

可是我快要被s上面google的哏儿笑死了，2333333333333333

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