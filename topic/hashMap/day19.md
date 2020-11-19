# 第十八题
## 题目描述
给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

 

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
[前往答题](https://github.com/leetcode-pp/91alg-2/issues/45)

## 个人解答

**思路:**
主要是哈希表做记录减少二次循环的问题。
每走过一个值就记录target-value ，后面如果有这个结果就直接返回。
**代码:**
javascript
``` javascript
var twoSum = function(nums, target) {
  let hashMap = new Map()
  const len = nums.length
  for (let i = 0; i < len; i++) {
    const node = nums[i];
    let ind = hashMap.get(node)
    if (ind!==undefined) return [ind,i]
    hashMap.set(target-node,i)
  }
  return []
}
```

**复杂度分析:**
时间复杂度O(n)
空间复杂度O(n)
 
**模板**
```javascript
let hashMap = new Map()
for(let key in arr){
  if (hashMap.get(arr[key])!==undefined) return arr[key]
}
```