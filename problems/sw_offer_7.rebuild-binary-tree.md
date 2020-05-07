### 题目地址

https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/

### 题目描述

#### ###7.重建二叉树

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。
假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
例如，给出
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
输出 [3,9,20,null,null,15,7]


### 思路

前序遍历特点： 节点按照 [ 根节点 | 左子树 | 右子树 ] 排序，以题目示例为例：[ 3 | 9 | 20 15 7 ]
中序遍历特点： 节点按照 [ 左子树 | 根节点 | 右子树 ] 排序，以题目示例为例：[ 9 | 3 | 15 20 7 ]
根据题目描述输入的前序遍历和中序遍历的结果中都不含重复的数字，其表明树中每个节点值都是唯一的。

根据以上特点，可以按顺序完成以下工作：

前序遍历的首个元素即为根节点 root 的值；
在中序遍历中搜索根节点 root 的索引 ，可将中序遍历划分为 [ 左子树 | 根节点 | 右子树 ] 。
根据中序遍历中的左（右）子树的节点数量，可将前序遍历划分为 [ 根节点 | 左子树 | 右子树 ]  。

自此可确定 三个节点的关系 ：1.树的根节点、2.左子树根节点、3.右子树根节点（即前序遍历中左（右）子树的首个元素）。

子树特点： 子树的前序和中序遍历仍符合以上特点，以题目示例的右子树为例：前序遍历：[20 | 15 | 7]，中序遍历 [ 15 | 20 | 7 ] 。

根据子树特点，我们可以通过同样的方法对左（右）子树进行划分，每轮可确认三个节点的关系 。此递推性质让我们联想到用 递归方法 处理。

### 关键点解析

递归 二叉树 

### 代码

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    //建一个哈希表用于搜索根节点root在中序遍历中的索引，时间复杂度降到O(1)需额外空间O(N)
    HashMap<Integer, Integer> dic = new HashMap<>();
    int[] tmp;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        tmp = preorder;
        //初始化哈希表
        for(int i = 0; i < inorder.length; i++) {
            dic.put(inorder[i],i);
        }
        //设置首次递归参数
        return recur(0,0,inorder.length-1);
    }
    //递归参数:前序遍历中根节点索引pre_root;中序遍历中的左边界in_left;中序遍历中的右边界in_right
    TreeNode recur(int pre_root, int in_left, int in_right) {
        //终止条件in_left > in_right，此时越过叶子节点返回null
        if(in_left > in_right) return null;
        //递归工作
        //a. 建根节点root，值为pre_root节点值
        TreeNode root = new TreeNode(tmp[pre_root]);
        //b. 搜索root节点在中序遍历中的索引
        int i = dic.get(tmp[pre_root]);
        //c. 假定root存在左右子树，构建二叉树开启下一级递归
        //   左子树recur(pre_root+1, in_left, i-1)
        //   右子树recur(i-in_left+pre_root+1, i+1, in_right)
        root.left = recur(pre_root+1, in_left, i-1);
        root.right = recur(i-in_left+pre_root+1, i+1, in_right);
        return root;
    }
}
```

### 拓展
暂无
