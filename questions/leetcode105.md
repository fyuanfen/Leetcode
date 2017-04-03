---
title: Leetcode-105-Construct-binary-tree-from-preorder-and-inorder-traversal
date: 2017-04-03 17:17:14
categories: 
- Code
tags:
- Leetcode

---

# 重建二叉树
## 题目描述
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

## 解法：

明白由先序遍历和中序遍历生成二叉树的过程就好了。首先找到先序遍历的第一个节点，就是根节点，然后在中序遍历中找到根节点。

此时，根节点左右两边，分别是左右子树的中序遍历。
再对于先序遍历，从第二个节点开始，到中序遍历中左子树的长度，就是左子树的先序遍历。
同理，右子树也是一样，这是一个递归过程。
## java解法：

```java
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        TreeNode root=reConstructBinaryTree(pre,0,pre.length-1,in,0,in.length-1);
        return root;
    }
    //前序遍历{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}
    private TreeNode reConstructBinaryTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn) {
         
        if(startPre>endPre||startIn>endIn)
            return null;
        TreeNode root=new TreeNode(pre[startPre]);
         
        for(int i=startIn;i<=endIn;i++)
            if(in[i]==pre[startPre]){
                root.left=reConstructBinaryTree(pre,startPre+1,startPre+i-startIn,in,startIn,i-1);
                root.right=reConstructBinaryTree(pre,i-startIn+startPre+1,endPre,in,i+1,endIn);
            }
                 
        return root;
    }
}

```

这里要注意，因为js是弱类型语言，所以判断为空的时候要尤其小心。
传入的参数可能为undefined，null或者空对象(数组也是对象)，所以需要排除这几种情况。

1. !pre判断是否为null和undefinded，
2. 检测是否为空要遍历对象的属性。

如下所示:
```javascript
/*
 * 检测对象是否是空对象(不包含任何可读属性)。
 * 方法既检测对象本身的属性，也检测从原型继承的属性(因此没有使hasOwnProperty)。
 */
function isEmpty(obj)
{
    for (var name in obj) 
    {
        return false;
    }
    return true;
};
```

因此异常检测代码如下：

```javascript
if(!pre || isEmpty(pre))
return;
```

## javascript解法
```javascript
function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} 
function build(pre, inorder, pstart, pend, istart, iend) {
    if (pstart > pend||istart>iend)return;
    var root = pre[pstart];
    
    for(var find = istart; find<=iend;find++){
         if(root === inorder[find]){
               break;
            }
    }
    var len = find-istart;//左子树长度
    var res = new TreeNode(inorder[find]);
    res.left = build(pre, inorder, pstart+1, pstart+len,istart,find-1);
    res.right = build(pre, inorder ,pstart+len+1, pend,find+1, inorder.length-1);
    return res;
}
function reConstructBinaryTree(pre, vin)
{
    if(!pre || isEmpty(pre))
return;
    return build(pre, vin, 0, pre.length-1, 0, vin.length -1);
    
}

```

## 解法2：
```javascript
/* function TreeNode(x) {
    this.val = x;
    this.left = null;
    this.right = null;
} */
function reConstructBinaryTree(pre, vin)
{
    // write code here
    if (!pre || pre.length === 0) {
        return;
    }
    var treeNode = {
        val: pre[0]
    }
    for(var i = 0; i < pre.length; i++) {
        if (vin[i] === pre[0]) {
            treeNode.left = reConstructBinaryTree(pre.slice(1, i+1), vin.slice(0, i));
            treeNode.right = reConstructBinaryTree(pre.slice(i+1),vin.slice(i+1));
        }
    }
    return treeNode;
    console.log(treeNode)
}

```
