# 第九题
## 题目描述
题目描述
给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：
```
      0
     / \
   -3   9
   /   /
 -10  5
```
[前往答题](https://github.com/leetcode-pp/91alg-2/issues/32)

## 个人解答

**思路:**
1、平衡二叉搜索树root为中值、单链表中间的节点为中值。
2、取单链表中间节点，很简单，快慢指针。
3、每次取链表中值做root,左边单独做左子树，右边单独做右子树，明显的分治思想。

**代码:**
javascript
``` javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {ListNode} head
 * @return {TreeNode}
 */
var sortedListToBST = function(head) {
  if (!head) return null
  function getRoot(head,over){
    if (head == over) return null
    let fast = head,slow=head
    while(fast.next&&fast.next!=over){
      fast = fast.next
      if (fast.next&&fast.next!=over) fast = fast.next
      slow= slow.next
    }
    let treeNode = new TreeNode(slow.val);
    treeNode.left = getRoot(head,slow)
    treeNode.right = getRoot(slow.next,over)
    return treeNode
  }
  return getRoot(head,null)
};
```

**复杂度分析:**
这波还真不会分析了，等结果

**模板：** 
1、快慢指针
``` javascript
let fast = head,slow=head
while(fast.next){
  fast = fast.next
  if (fast.next) fast = fast.next
  slow= slow.next
}
```
2、分治
``` javascript
function conquer(arr,start,end){
  let index = XXXXX
  return [...conquer(arr,start,index),arr[index],...conquer(arr,index+1,end)]
}
conquer(arr,0,arr.length)
```