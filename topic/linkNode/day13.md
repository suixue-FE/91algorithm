# 第十三题
## 题目描述
定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
来源：力扣（LeetCode）
链接：leetcode-cn.com/problems/maximum-depth-of-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/38)

## 个人解答

**思路:**

不太想写递归了，之前写过这道题所以写下自己不熟悉的方案-bfs
1、搞一个队列，开始只把root放进去，也就是放进去第一层
2、把第一层shift() 出来，看第一层的左右节点，存在就放进去
3、依次向下推，直到某一层没有节点就是最深的
bfs，广度优先，每到一层就把这层所有的节点全收起来，并把上一层的删掉，直到缓存的队列空了。
**代码:**
javascript
``` javascript
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
  if (root === null) return 0
  let queue = [root],result = 0
  while (queue.length){
    result++
    const qLen = queue.length
    for (let i = 0; i < qLen;i++){
      const node = queue.shift()
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
  }
  return result
}
```

**复杂度分析:**
时间复杂度O(n*m)
空间复杂度O(n)
 
**模板**
``` javascript
bfs(root){
	let queue = []
  queue.push(root)
  while(queue.length){
  	const queLen = queue.length
    for(let i = 0;i++;i<queLen){
      const node = queue.shift()
    	XXXXX(node)      //  处理逻辑，比如放入数组
      if(node.left) queue.push(node.left)
      if(node.right) queue.push(node.right)
    }
  }
}
```