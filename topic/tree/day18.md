# 第十八题
## 题目描述
给定二叉树，按垂序遍历返回其结点值。

对位于 (X, Y) 的每个结点而言，其左右子结点分别位于 (X-1, Y-1) 和 (X+1, Y-1)。

把一条垂线从 X = -infinity 移动到 X = +infinity ，每当该垂线与结点接触时，我们按从上到下的顺序报告结点的值（ Y 坐标递减）。

如果两个结点位置相同，则首先报告的结点值较小。

按 X 坐标顺序返回非空报告的列表。每个报告都有一个结点值列表。

 

示例 1：



输入：[3,9,20,null,null,15,7]
输出：[[9],[3,15],[20],[7]]
解释： 
在不丧失其普遍性的情况下，我们可以假设根结点位于 (0, 0)：
然后，值为 9 的结点出现在 (-1, -1)；
值为 3 和 15 的两个结点分别出现在 (0, 0) 和 (0, -2)；
值为 20 的结点出现在 (1, -1)；
值为 7 的结点出现在 (2, -2)。
示例 2：



输入：[1,2,3,4,5,6,7]
输出：[[4],[2],[1,5,6],[3],[7]]
解释：
根据给定的方案，值为 5 和 6 的两个结点出现在同一位置。
然而，在报告 "[1,5,6]" 中，结点值 5 排在前面，因为 5 小于 6。
 

提示：

树的结点数介于 1 和 1000 之间。
每个结点值介于 0 和 1000 之间。
https://leetcode-cn.com/problems/vertical-order-traversal-of-a-binary-tree/
[前往答题](https://github.com/leetcode-pp/91alg-2/issues/44)

## 个人解答

**思路:**
主要是记录x和y然后排序
记录x和y的过程就是遍历树的过程，可以自行选择dfs或者bfs
**代码:**
javascript
``` javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var verticalTraversal = function(root) {
  if(!root) return []
  function verticalObj(node,obj,x=0,y = 0){
    if(obj[x]) obj[x].push({key:y,val:node.val})
    else obj[x]=[{key:y,val:node.val}]
    if (node.left) verticalObj(node.left,obj,x-1,y-1)
    if (node.right) verticalObj(node.right,obj,x+1,y-1)
  }
  let object = {}
  verticalObj(root,object)
  let arr = Object.keys(object)
  arr.sort((a,b)=>a-b)
  const aLen = arr.length
  let result = new Array(aLen)
  for (let i = 0; i < aLen; i++) {
    result[i] = object[arr[i]].sort((a,b)=>{
      if (a.key==b.key) return a.val-b.val
      return b.key-a.key
    }).map(val=>val.val)
  }
  return result
};
```

**复杂度分析:**
时间复杂度O(n)
空间复杂度O(n)
 
**模板**
bfs/dfs都行，主要是记录x、y
