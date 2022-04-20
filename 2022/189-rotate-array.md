### 题目地址
https://leetcode-cn.com/problems/rotate-array/

### 题目描述
给你一个数组，将数组中的元素向右轮转 k 个位置，其中 k 是非负数。

示例 1:
```shell
输入: nums = [1,2,3,4,5,6,7], k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右轮转 1 步: [7,1,2,3,4,5,6]
向右轮转 2 步: [6,7,1,2,3,4,5]
向右轮转 3 步: [5,6,7,1,2,3,4]
```

示例 2:
```shell
输入：nums = [-1,-100,3,99], k = 2
输出：[3,99,-1,-100]
解释: 
向右轮转 1 步: [99,-1,-100,3]
向右轮转 2 步: [3,99,-1,-100]
```

### 思路
写一个反转字符串区间函数，先反转【0，n-1】 再【0，k-1】，最后【k,n-1】
e.g [1,2,3,4,5,6,7],k=3-> [7654321] -> [5674321] -> [5671234]

### 关键点解析


### 代码

```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        # 防止k过大返回异常
        k %= n
        def reverse(i ,j):
            while i < j:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
                j -= 1
        reverse(0,n-1)
        reverse(0, k-1)
        reverse(k,n-1)

if __name__ == '__main__':
    s = Solution()

```

### 拓展

