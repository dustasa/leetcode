### 题目地址
https://leetcode-cn.com/problems/move-zeroes/

### 题目描述
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

请注意 ，必须在不复制数组的情况下原地对数组进行操作。

示例1：
```shell
输入: nums = [0,1,0,3,12]
输出: [1,3,12,0,0]
```
示例2:
```shell
输入: nums = [0]
输出: [0]
```

### 思路
记录有多少个零，然后相应非0的元素往前移动count个单位； 最后把后面的全部置为0
### 关键点解析
注意对应元素前有几个0就应当移动几位

### 代码

```python
# 解法1
class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        count = 0
        # 记录有多少个零，然后相应非0的元素往前移动count个单位； 最后把后面的全部置为0
        for i in range(0,n):
            if (nums[i] == 0):
                count += 1
            else:
                nums[i-count] = nums[i]

        for k in range(n-count,n):
            nums[k] = 0


if __name__ == '__main__':
    s = Solution()

```

### 拓展

