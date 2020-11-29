# 第二十五题
## 题目描述
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

示例 1:

输入: [1,3,5,6], 5
输出: 2
示例 2:

输入: [1,3,5,6], 2
输出: 1
示例 3:

输入: [1,3,5,6], 7
输出: 4
示例 4:

输入: [1,3,5,6], 0
输出: 0
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/search-insert-position
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/51)

## 个人解答

**思路:**

很简单的二分，和有序数组查找某值很像，但是边界还是处理了很久

**代码:**
javascript
``` javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
  const len = nums.length
  if (len == 0) return 0
  let l=0,r=len
  while (l<r){
    if (r-l==1) return nums[l]>=target?l:r
    let middle = Math.floor((l+r)/2)
    if (nums[middle]==target) return middle
    if (nums[middle]>target) r=middle  
    if (nums[middle]<target) l=middle  
  }
  return nums[l]>=target?l:l+1
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(logn)
空间复杂度：O(1)

