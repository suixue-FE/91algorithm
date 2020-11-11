# 第十题
## 题目描述
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。
 

示例 1：

输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。

示例 2：

输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。

示例 3：

输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。

进阶：
你是否可以不用额外空间解决此题？

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/34)

## 个人解答

**思路1:**

昨天解题差点忘了之前最早的链表相交循环我都是直接用哈希表解答的
1. 遍历链表并存储。
2. 遍历链表过程中查看哈希表，哈希表中存在的就是入口。

**代码1:**
javascript
``` javascript
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function(head) {
  let stack = new Map();
  let cur = head
  while(cur){
    if (stack.get(cur)) {
      return cur;
    }else{
     stack.set(cur, true);
    }
    cur = cur.next;
  }
  return null;
};
```

**复杂度分析1:**
时间复杂度O(n)
空间复杂度O(n)

**思路2:**

快指针和慢指针再环内相遇的点，到环的起始点的距离和head指针到起始点的距离是一样的,这里有套数学公式计算:<
快指针走的距离 fastLength， 慢指针距离 slowLength，head到环的起始点 F, 环的起始点到相遇点 a, 相遇点到环的起始点 b
```
fastLength = 2*slowLength
F+a+b+a = 2*(F+a)
F=b
```
总之记住模板  快慢指针得到初次相遇点 -> 慢指针和头部指针一起走 -> 两个会在环形入口点相遇

**代码2:**
javascript
``` javascript
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function(head) {
  let start = head
  let fast = head
  let slow = head
  while(fast && fast.next){
    fast = fast.next.next
    slow = slow.next
    if (slow == fast) {
      while (slow != start){
        slow=slow.next
        start = start.next
      }
      return start
    }
  }
  return null
};
```

**复杂度分析2:**
时间复杂度O(n)
空间复杂度O(1)
**模板：** 
链表环形入口点模板
``` javascript
while(fast && fast.next){
    fast = fast.next.next
    slow = slow.next
    if (slow == fast) {
      while (slow != start){
        slow=slow.next
        start = start.next
      }
      return start
    }
  }
```