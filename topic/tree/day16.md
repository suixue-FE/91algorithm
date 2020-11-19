# 第十六题
## 题目描述
给定一个二叉树，在树的最后一行找到最左边的值。

示例 1:

输入:

    2
   / \
  1   3

输出:
1
 

示例 2:

输入:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

输出:
7
注意: 您可以假设树（即给定的根节点）不为 NULL。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-bottom-left-tree-value
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/41)

## 个人解答

**思路1:**

个人只想出了BFS的解法
1、我们需要找到最后一层的第一个值，最好的方法就是层序遍历，遍历到最后一层
2、每次遍历开始把第一个值存起来，直到最后就是最后一层的第一个值了
**代码1:**
javascript
``` javascript
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findBottomLeftValue = function(root) {
  if (!root) return null;
  let queue = [root],alsp = null
  while (queue.length){
    alsp = queue[0].val;
    const qLen = queue.length
    for (let i = 0; i < qLen; i++) {
      const node = queue.shift()
      if (node.left) queue.push(node.left)
      if (node.right) queue.push(node.right)
    }
  }
  return alsp
};
```

**复杂度分析1:**
时间复杂度O(n)
空间复杂度O(n)
 
**模板**
bfs模板

**思路2:**

就是知道想用DFS但是依然没有思路，看了优秀童鞋的解答
1、递归查找，从右子树到左子树，以数组存储每一层的数据。
2、因为是从右到左调用，直接把当前层数据覆盖最后得到的就是当前层最左侧数据。
3、直接返回数组最后一项，此项代表树最后一层的最左侧。
其实本质也是存储每一项的最左侧，就是遍历方式不一样而已，就是想不出，还需锻炼。
**代码1:**
javascript
``` javascript
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findBottomLeftValue = function(root) {
  if (!root) return null
  let leftMostLayer = [];
  traverse(root, leftMostLayer, 0);
  return leftMostLayer[leftMostLayer.length - 1];
 };
 
 function traverse(root, leftMost, layer) {
  if (root) {
    leftMost[layer++] = root.val;
    traverse(root.right, leftMost, layer);
    traverse(root.left, leftMost, layer);
  }
}
```

**复杂度分析1:**
时间复杂度O(n)
空间复杂度O(n)
 
**模板**
dfs模板