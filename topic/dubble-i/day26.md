# 第二十六题
## 题目描述
编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。
 

示例 1：


输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,50]], target = 3
输出：true
示例 2：


输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,50]], target = 13
输出：false
示例 3：

输入：matrix = [], target = 0
输出：false
 

提示：

m == matrix.length
n == matrix[i].length
0 <= m, n <= 100
-104 <= matrix[i][j], target <= 104

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/search-a-2d-matrix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/52)

## 个人解答

**思路:**

这不还是一个很简单的二分，直接抻平然后二分，结束。

**代码:**
javascript
``` javascript
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
  const arr = matrix.flat()
  let l = 0 ,r = arr.length - 1
  while (l<=r) {
    const middle = Math.floor((l+r)/2);
    const value = arr[middle]
    if (value == target) return true
    if (value<target){
      l = middle + 1
      continue
    } 
    if (value>target){
      r = middle - 1
      continue
    } 
  }
  return false
};
```

**复杂度分析:**
时间复杂度：O(log(m*n))
空间复杂度：O(m*n)

