# 题目描述
操作给定的二叉树，将其变换为源二叉树的镜像。 
## 输入描述:
二叉树的镜像定义：源二叉树 

```
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
```    	
    	
## 解题思路：
利用递归即可解决	

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