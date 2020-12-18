**思路:**
1. 一直记得树是最适合递归的结构，拿到直接先想的递归
2. 判断节点是否全部为0，如果全部为0，就返回null
3. 全部为0就是root.val等于0，root的子节点都返回了null

**代码:**
javascript
``` javascript
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var pruneTree = function(root) {
  if (!root) return null
  let nodeLeft = pruneTree(root.left)
  let nodeRight = pruneTree(root.right)
  if (root.val!==1&&!nodeLeft&&!nodeRight){
    return null
  }
  root.left = nodeLeft
  root.right = nodeRight
  return root
}
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n)
空间复杂度：O(1) 好像是，不太会算了突然