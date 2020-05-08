### 题目地址

无

### 题目描述

#### 7.二叉树的下一个节点

```shell

给定二叉树和其中一个节点
如何找出中序遍历中的下一个节点?

eg.给一个二叉树：
	        a
               /  \
              b    c
             / \  / \
            d  e f  g
                / \
               h   i



中序遍历： [d,b,h,e,i,a,f,c,g]
```

### 思路

中序遍历特点：

中序遍历特性： 左|根|右

1. 节点有右子树，下一个节点为右子树的最左子节点
	b-> e->h, c->g,a->f
2. 节点没有右子树(d, h, i, f, g)
	i.  如果该节点是父节点的左子节点(d , h ,f):
	    中序遍历中下一个节点就为该节点的父节点
	    d->b, h->e, f->c 
	ii. 如果该节点是父节点的右子节点(i, g):
	    沿父节点的指针一直向上遍历，直到找到一个既是它的父节点又是左子节点的节点，
	    若该节点的父节点存在，则该节点的父节点即为中序遍历中的下一个节点
	    i-> e ->b->a 
	    若该节点的父节点不存在，则说明所求节点无下一个节点
	    g->c->a-> null


### 关键点解析

中序遍历 二叉树 

### 代码

```c++
/**
 * Definition for a binary tree node.
 * struct BinaryTreeNode
 * {
 *     int val;
 *     BinaryTreeNode* left;
 *     BinaryTreeNode* right;
 *     BinaryTreeNode* parent;
 * };
 */
 BinaryTreeNode* GetNext(BinaryTreeNode* pNode)
{
    //非空检查
    if(pNode == nullptr)
    {
	return nulptr;
    }
    //pNext即为pNode下一个节点
    BinaryTreeNode* pNext = nullptr;
    //判断pNode是否有右子树
    if(pNode->right != nullptr)
    {
    	 //有右子树则将右子树的最左节点返回
	 BinaryTreeNode* pRight = pNode->right;
	 while(pRight->left != null)
	 {
		pRight = pRight->left;
	 }
	 pNext = pRight;
    }
    //pNode没有右子树,沿父节点遍历向上
    else if(pNode->parent != nullptr)
    {
	BinaryTreeNode* pCurrent = pNode;
	BinaryTreeNode* pParent = pNode->parent;
	//当遍历的节点不空且为对应父节点的右子节点时，向上查找
	while(pParent != nullptr && pCurrent == pParent->right)
	{
	    pCurrent = pParent;
	    pParent = pParent->parent;
	}
	pNext = pParent;
    }
    return pNext;
}
```

### 拓展
暂无
