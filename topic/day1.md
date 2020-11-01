# 第一题
## 题目藐视
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。
最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。
你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:
输入: [1,2,3]
输出: [1,2,4]
解释: 输入数组表示数字 123。

示例 2:
输入: [4,3,2,1]
输出: [4,3,2,2]
解释: 输入数组表示数字 4321。

来源：力扣（LeetCode）
链接：leetcode-cn.com/problems/plus-one
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/lisansang/91algorithm/issues/1)

## 个人解答

**思路:**

1. 数学思路，从个位加一，满10进1。数组就是从最后一位加 1 ，满10进1。
2. 代码逻辑就是满10的时候当前为变为0，继续循环前一位+1，不满10就直接return。
3. 可能全部位满10，则循环完毕后第一位会是0，直接在数组头部添加一个  1 即可

**代码:**
javascript
``` javascript
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
  for (let i = digits.length-1; i >= 0; i--){
    digits[i]++
    if (digits[i]!==10) return digits
    digits[i] = 0
  }
  if (digits[0]===0) digits.unshift(1)
  return digits
};
```

**复杂度分析:**
n为数组长度
时间复杂度：最好情况O(1)，最坏情况O(n)
空间复杂度：O(n)

**模板：** 无 
