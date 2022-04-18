### 题目地址
https://leetcode-cn.com/problems/search-insert-position/
### 题目描述
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 O(log n) 的算法
### 思路

### 关键点解析

### 代码

```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left,right = 0, len(nums)-1

        while(left<= right):

            mid = (left+right) //2
            if(nums[mid] > target):
                # 向左查找
                right = mid-1
            elif (nums[mid] < target):
                # 向右查找
                left = mid+1
            else:
                return mid
        return right+1


if __name__ == '__main__':
    s = Solution()

```

### 拓展

