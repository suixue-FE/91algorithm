**思路:**
0. js怎么搞堆还是不太会
1. 整一个哈希表存出现了多少次
2. 按出现次数排序
3. 按排序从多到少插入数组，插入时带孔
4. 每次插入一次存储的值-1，减没了就下一个数

**代码:**
javascript
``` javascript
/**
 * @param {number[]} barcodes
 * @return {number[]}
 */
var rearrangeBarcodes = function(barcodes) {
  const bLen = barcodes.length
  const map = new Map();
  barcodes.forEach(value => {
    map.set(value,map.has(value) ? map.get(value)+1 : 1)
  })
  let arr = [...map].sort((a,b) => b[1]-a[1])
  let j = 0
  const result = new Array(bLen)
  for (let i = 0; i < bLen; i+=2) {
    let node = arr[j]
    result[i] = node[0]
    node[1]--
    if (node[1] === 0) j++
  }
  for (let k = 1; k < bLen; k+=2) {
    let node = arr[j]
    result[k] = node[0]
    node[1]--
    if (node[1] === 0) j++ 
  }
  return result
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n)
空间复杂度：O(n)