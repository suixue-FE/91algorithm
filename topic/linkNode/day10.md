# 第十题
## 题目描述
编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表：

image

在节点 c1 开始相交。

 

示例 1：
image

输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
 

示例 2：
image

输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
 

示例 3：
image

输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/33)

## 个人解答

**思路:**
又到了一年一度套模板的时间了，讲义合并链表几个模板，其中符合题目要求的O1空间的就是相交链表中的双指针模板。
- 例如使用 a, b 两个指针分别指向 A, B 这两条链表, 两个指针相同的速度向后移动,
- 当 a 到达链表的尾部时,重定位到链表 B 的头结点
- 当 b 到达链表的尾部时,重定位到链表 A 的头结点。
- a, b 指针相遇的点为相交的起始节点，否则没有相交点

为什么 a, b 指针相遇的点一定是相交的起始节点? 我们证明一下：
1. 将两条链表按相交的起始节点继续截断，链表 1 为: A + C，链表 2 为: B + C
2. 当 a 指针将链表 1 遍历完后,重定位到链表 B 的头结点,然后继续遍历直至相交点(a 指针遍历的距离为 A + C + B)
3. 同理 b 指针遍历的距离为 B + C + A

**代码:**
javascript
``` javascript
/**
 * @param {ListNode} headA
 * @param {ListNode} headB
 * @return {ListNode}
 */
var getIntersectionNode = function(headA, headB) {
  let a = headA
  let b = headB
  while (a!==b) {
    a = a === null ? headB : a.next;
    b = b === null ? headA : b.next;
  }
  return a
};
```

**复杂度分析:**
时间复杂度O(n)
空间复杂度O(1)
**模板：** 
链表双指针
``` javascript
function(headA, headB) {
  let a = headA
  let b = headB
  while (a!==b) {
    a = a === null ? headB : a.next;
    b = b === null ? headA : b.next;
  }
  return a
}
```
这题完完全全套个模板啊，看了讲义就直接套了。