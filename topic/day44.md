**思路:**


**代码:**
javascript
``` javascript

// @lc code=start
/**
 * @param {number[][]} M
 * @return {number}
 */
var findCircleNum = function(M) {
  const len = M.length
  let visited = {};
  let result = 0
  let dfs = (node) => {
    for(let j = 0; j < len;j++){
      if(node[j] == 1 && !visited[j]){
          visited[j] = true;
          dfs(M[j]);
      }
    }
  }
  for (let i = 0; i < len;i++){
    if (!visited[i]) {
      dfs(M[i])
      result++
    }
  }
  return result
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n^2)
空间复杂度：O(n)

**模板：** 
```javascript
dfs(node)
function dfs(node){
  // 有时候需要存储个状态，一般不用，直接往下突就完事了
  if(node){
     // dosomething
  }
	node.children.forEach(val=>{
    dfs(val)
  })
}
```