**思路:**
0. 主要是把握easy的机会赶紧跟上
1. js怎么搞堆不太会啊，用的单调递增数组

**代码:**
javascript
``` javascript
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function(stones) {
  let stack = []
  stones.sort((a,b)=>a-b)
  while (stones.length>1){
    const res = stones.pop() - stones.pop()
    if (res>0) {
      let i = 0,sLen = stones.length
      while(i<sLen&&stones[i]<res){
        stack.push(stones.shift())
      }
      stones.unshift(res)
      while(stack.length>0){
        stones.unshift(stack.pop())
      }
    }
  }
  return stones.length?stones[0]:0
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n^2)
空间复杂度：O(n)