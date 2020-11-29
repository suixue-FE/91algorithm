# 第二十五题
## 题目描述
今天，书店老板有一家店打算试营业 customers.length 分钟。每分钟都有一些顾客（customers[i]）会进入书店，所有这些顾客都会在那一分钟结束后离开。

在某些时候，书店老板会生气。 如果书店老板在第 i 分钟生气，那么 grumpy[i] = 1，否则 grumpy[i] = 0。 当书店老板生气时，那一分钟的顾客就会不满意，不生气则他们是满意的。

书店老板知道一个秘密技巧，能抑制自己的情绪，可以让自己连续 X 分钟不生气，但却只能使用一次。

请你返回这一天营业下来，最多有多少客户能够感到满意的数量。
 

示例：

输入：customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], X = 3
输出：16
解释：
书店老板在最后 3 分钟保持冷静。
感到满意的最大客户数量 = 1 + 1 + 1 + 1 + 7 + 5 = 16.
 

提示：

1 <= X <= customers.length == grumpy.length <= 20000
0 <= customers[i] <= 1000
0 <= grumpy[i] <= 1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/grumpy-bookstore-owner
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/56)

## 个人解答

**思路:**

双指针滑动窗口

1. 小于X之前单指针计算可能拉回来的客户
2. 大于X之后双指针，前一个指针指向后一个指针-X 这样不用遍历就能直接O1复杂度计算新的拉回客户数
3. 遍历的同时计算如果不拉回客户会有多少客户


**代码:**
javascript
``` javascript
/**
 * @param {number[]} customers
 * @param {number[]} grumpy
 * @param {number} X
 * @return {number}
 */
var maxSatisfied = function(customers, grumpy, X) {
  const length = customers.length
  let allCustomer = 0,result = 0 ,max = 0
  for (let i = 0; i < length;i++){
    if (grumpy[i]==0) allCustomer +=customers[i]
    const guke = grumpy[i]==1?customers[i]:0
    if (i<X) result += guke
    else{
      const gukeBef = grumpy[i-X]==1?customers[i-X]:0
      result = result - gukeBef + guke
    }
    if (result > max) max = result;
  }
  return allCustomer + max
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n)
空间复杂度：O(1)

**套路**

```javascript
let result 
for (let i = 0; i < length;i++){
  if(i<X) result += arr[i]
  else{
    const j = i-X
    result = result+arr[i]-arr[j]
    }
  
}
```

