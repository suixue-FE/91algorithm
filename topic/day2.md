# 第二题
## 题目描述
给定一个字符串 S 和一个字符 C。返回一个代表字符串 S 中每个字符到字符串 S 中的字符 C 的最短距离的数组。

示例 1:

输入: S = "loveleetcode", C = 'e'
输出: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]
说明:

字符串 S 的长度范围为 [1, 10000]。
C 是一个单字符，且保证是字符串 S 里的字符。
S 和 C 中的所有字母均为小写字母。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shortest-distance-to-a-character
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/16)

## 个人解答

**思路:**

第一步：遍历存起来一个包含所有c的数组
第二步：再遍历一次去计算距离，计算距离有很大优化空间

* i在第一个c之前，距离= 第一个c-i
* i在两个c中间，取min(后一个c-i，i-前一个c)
* i在最后一个c之后，距离=i-最后一个c
这样优化之后就不用再遍历存起来的C数组了

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
