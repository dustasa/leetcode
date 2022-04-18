### 题目地址
https://leetcode-cn.com/problems/binary-search/
### 题目描述
给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

### 思路
二分查找
### 关键点解析
注意冒号，很久没手写python了
### 代码

```python
# 暴力解法
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        i = 0
        tmp = -1
        for i in range(0, len(nums)):
            if nums[i] == target:
                tmp = i
            else:
                i = i+1
        return tmp

if __name__ == '__main__':
    solution = Solution()

```

### 拓展
改进二分查找,注意左右对齐
，如果说定义 target 是在一个在左闭右开的区间里，也就是[left, right) ，那么二分法的边界处理方式则截然不同。
有如下两点：

while (left < right)，这里使用 < ,因为left == right在区间[left, right)是没有意义的
if (nums[middle] > target) right 更新为 middle，因为当前nums[middle]不等于target，去左区间继续寻找，而寻找区间是左闭右开区间，所以right更新为middle，即：下一个查询区间不会去比较nums[middle]
在数组：1,2,3,4,7,9,10中查找元素2，

（版本一）左闭右闭区间
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums) - 1
        
        while left <= right:
            middle = (left + right) // 2

            if nums[middle] < target:
                left = middle + 1
            elif nums[middle] > target:
                right = middle - 1
            else:
                return middle
        return -1
```
（版本二）左闭右开区间
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left,right  = 0, len(nums)
        while left < right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid+1
            elif nums[mid] > target:
                right = mid
            else:
                return mid
        return -1
```