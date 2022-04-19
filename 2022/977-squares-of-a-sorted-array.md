### 题目地址
https://leetcode-cn.com/problems/squares-of-a-sorted-array/
### 题目描述
给你一个按 非递减顺序 排序的整数数组 nums，返回 每个数字的平方 组成的新数组，要求也按 非递减顺序 排序。

示例 1：

输入：nums = [-4,-1,0,3,10]
输出：[0,1,9,16,100]

解释：平方后，数组变为 [16,1,0,9,100]
排序后，数组变为 [0,1,9,16,100]

示例 2：

输入：nums = [-7,-3,2,3,11]
输出：[4,9,9,49,121]

### 思路
数组其实是有序的， 只不过负数平方之后可能成为最大数了。

那么数组平方的最大值就在数组的两端，不是最左边就是最右边，不可能是中间。

此时可以考虑双指针法了，i指向起始位置，j指向终止位置。

定义一个新数组result，和A数组一样的大小，让k指向result数组终止位置。
### 关键点解析

### 代码

```python
# 暴力解法 待优化
# 内存消耗：15.1 MB, 在所有 Python 提交中击败了7.19% 的用户。。。。

class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        ans = []
        for i in range(0, len(nums)):
            ans.append(nums[i] ** 2)
        # ans从小到大排序
        ans.sort(reverse=False)
        return ans


if __name__ == '__main__':
    s = Solution()

```

```python
# 改进一，貌似并没有好多少
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        ans = []
        left, right  = 0,len(nums)
    
        mid = (left+right) //2
        if (nums[mid] >= 0):
            for i in range(mid,right):
                ans.append(nums[i] ** 2)
            for j in range(left,mid):
                ans.append(nums[j] ** 2)
        else:
            for k in range(left,right):
                ans.append(nums[k] ** 2)  

        ans.sort(reverse=False)
        return ans

if __name__ == '__main__':
    s = Solution()
```

```python
# 双指针法
# sota
class Solution(object):
    def sortedSquares(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n  = len(nums)
        ans = [-1] * n
        # 头、尾部、当前指针
        i,j,k = 0,n - 1,n - 1
        while i <= j:
            # 计算左边平方最大
            lm = nums[i] ** 2
            # 计算右边平方最大
            rm = nums[j] ** 2
            if lm > rm:
                ans[k] = lm
                i += 1
            else:
                ans[k] = rm
                j -= 1
            k -= 1
        return ans

if __name__ == '__main__':
    s = Solution()
```

### 拓展

