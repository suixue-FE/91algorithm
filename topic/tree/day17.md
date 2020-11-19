# 第十七题
## 题目描述
请实现两个函数，分别用来序列化和反序列化二叉树。

示例: 

你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/43)

## 个人解答

**思路:**

bfs很简单，不知道dfs能不能写，我觉得没必要强行dfs了吧，就很适合bfs。
1. 序列化：层序遍历，检测到没有就加个null进去。
2. 序列化：还有一点要注意，就是最后一层全是null的时候不能加进去，不然多一层null。
3. 反序列化也很有意思，就是想办法按照序列化时的队列变化情况构建队列。
**代码:**
javascript
``` javascript
/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function(root) {
  if (!root) return '[]'
  let queue = [root], qLen = 1,resArr=`[${root.val},`
  while (qLen){
    let arrNow = ''
    for (let i = 0; i < qLen; i++) {
      const node = queue.shift()
      if (node.left) {
        queue.push(node.left)
        arrNow = arrNow + node.left.val + ','
      }else arrNow=arrNow + 'null,'
      if (node.right) {
        queue.push(node.right)
        arrNow = arrNow + node.right.val + ','
      }else arrNow=arrNow + 'null,'
    }
    qLen = queue.length
    if (qLen!==0) resArr = resArr+arrNow
  }
  return `${resArr.slice(0,-1)}]`
};

/**
* Decodes your encoded data to tree.
*
* @param {string} data
* @return {TreeNode}
*/
var deserialize = function(data) {
  if(data == "[]") return null
  let list = data.slice(1,-1).split(',')
  let root =  new TreeNode(list.shift())
  let queue = [root]
  while(queue.length&&list.length){
    const qLen = queue.length
    for (let i = 0; i < qLen; i++){
      const node = queue.shift()
      const left = list.shift()
      const right = list.shift()
      if (left&&left != 'null') {
        node.left =  new TreeNode(left)
        queue.push(node.left)
      }
      if (right&&right != 'null') {
        node.right =  new TreeNode(right)
        queue.push(node.right)
      }
    }
  }
  return root
};
```

**复杂度分析:**
时间复杂度O(n)
空间复杂度O(n)
 
**模板**
bfs模板