### 题目地址

```shell
https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof
```

### 题目描述

#### 9.用两个栈实现队列

```shell

队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead分别完成在队列尾部插入整数和在队列头部删除整数的功能。
(若队列中没有元素，deleteHead 操作返回 -1 )

示例 1：

输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]


示例 2：

输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]

```

### 思路
```shell
维护两个栈，第一个栈存储元素，第二个栈用于辅助操作。

插入元素时我们将其压入第一个栈，这样第一个栈的栈底应为队列头部元素，
在进行删除队头节点操作时，进行判断：
    a. 第二个栈为空且第一个栈不为空时：
        将第一个栈的元素全部弹出再压入第二个栈，实现对栈一元素的逆序
    b. 第二个栈为空且第一个栈为空时：
        返回-1
    c.  第二个栈不为空时不管第一个栈的状态，直接输出栈二栈顶元素即为队列头节点元素

```
### 关键点解析
```shell
栈 队列 
```
### 代码

```java
class CQueue {
    Stack<Integer> stack1;
    Stack<Integer> stack2;
    //创建一个队列
    public CQueue() {
        stack1 = new Stack<Integer>();
        stack2 = new Stack<Integer>();
    }
    //实现在队列尾部插入整数
    public void appendTail(int value) {
        //将元素插入stack1
        stack1.push(value);
    }
    //实现在队列头部删除整数
    public int deleteHead() {
        if (stack2.size() <= 0){
            while (stack1.size() > 0) {
                //将stack1中的元素弹出再压入stack2将栈内元素顺序逆序
                int tmp = stack1.pop();
                stack2.push(tmp);
            }
        }
        if (stack2.size() == 0) {
            return -1;
        }
        int head = stack2.pop();
        return head;
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */

```
### 拓展

暂无
