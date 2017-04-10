# 链表中倒数第k个结点
## 题目描述
输入一个链表，输出该链表中倒数第k个结点。

## 解法：
为了能够只遍历一次就能找到倒数第k个节点，可以定义两个指针：

1. 第一个指针从链表的头指针开始遍历向前走k，第二个指针保持不动；

2. 从第k+1步开始，第二个指针也开始从链表的头指针开始遍历；

3. 由于两个指针的距离保持在k，当第一个（走在前面的）指针到达链表的尾结点的下一个结点（也就是倒数第0个结点，即null值）时，第二个指针（走在后面的）指针正好是倒数第k个结点。
　　
## 代码完善：　
**思路很简单，但是这里要考虑3处鲁棒性问题：**

1. 输入的head为空指针。由于代码会试图访问空指针指向的内存，程序崩溃。

	解决：在处理前增加判断空指针的代码

2. 输入的以head为头结点的链表的结点总数少于k。由于在for循环中会在链表上向前走k步，仍然会由于空指针造成程序崩溃。

　　解决：在for循环中增加判断下一个节点是否是空指针的代码

## 代码：　　
```javascript　　
function ListNode(x){
    this.val = x;
    this.next = null;
}


function FindKthToTail(head, k)
{
    if(head == null || k <= 0){
        return null;
    }
    var p = head,
        q = p,
        count = 0;
    while(q!=null && count < k) {
        count++;
        q = q.next;
    }
    if(count === k){//移动了k次
        while(q!=null){//判断是否已经移到了末尾
            p = p.next;
            q = q.next;
        }
        return p;
    }
    else{
        return null;
    }
}
```