# 第三题
## 题目描述
请你设计一个支持下述操作的栈。

实现自定义栈类 CustomStack ：

CustomStack(int maxSize)：用 maxSize 初始化对象，maxSize 是栈中最多能容纳的元素数量，栈在增长到 maxSize 之后则不支持 push 操作。
void push(int x)：如果栈还未增长到 maxSize ，就将 x 添加到栈顶。
int pop()：弹出栈顶元素，并返回栈顶的值，或栈为空时返回 -1 。
void inc(int k, int val)：栈底的 k 个元素的值都增加 val 。如果栈中元素总数小于 k ，则栈中的所有元素都增加 val 。

示例：

输入：
["CustomStack","push","push","pop","push","push","push","increment","increment","pop","pop","pop","pop"]
[[3],[1],[2],[],[2],[3],[4],[5,100],[2,100],[],[],[],[]]
输出：
[null,null,null,2,null,null,null,null,null,103,202,201,-1]
解释：
CustomStack customStack = new CustomStack(3); // 栈是空的 []
customStack.push(1); // 栈变为 [1]
customStack.push(2); // 栈变为 [1, 2]
customStack.pop(); // 返回 2 --> 返回栈顶值 2，栈变为 [1]
customStack.push(2); // 栈变为 [1, 2]
customStack.push(3); // 栈变为 [1, 2, 3]
customStack.push(4); // 栈仍然是 [1, 2, 3]，不能添加其他元素使栈大小变为 4
customStack.increment(5, 100); // 栈变为 [101, 102, 103]
customStack.increment(2, 100); // 栈变为 [201, 202, 103]
customStack.pop(); // 返回 103 --> 返回栈顶值 103，栈变为 [201, 202]
customStack.pop(); // 返回 202 --> 返回栈顶值 202，栈变为 [201]
customStack.pop(); // 返回 201 --> 返回栈顶值 201，栈变为 []
customStack.pop(); // 返回 -1 --> 栈为空，返回 -1

提示：

1 <= maxSize <= 1000
1 <= x <= 1000
1 <= k <= 1000
0 <= val <= 100
每种方法 increment，push 以及 pop 分别最多调用 1000 次

来源：力扣（LeetCode）
链接：leetcode-cn.com/problems/design-a-stack-with-increment-operation
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/17)

## 个人解答

**思路一:**
数组模拟栈
push 时size+1 当size=maxSize是不许入栈
pop 时size-1 当size=0时return -1
in 时循环给元素增加val
**代码:**
太简单大家都会就不贴了，而且之前写过不太想写了
**复杂度分析:**
n为数组长度
时间复杂度：O(n)
空间复杂度：O(n)

**思路二:**
受评论大佬启发，个人完全没想到
主要是in() 时直接将k/size ： val 以哈希形式存储
pop（） 弹出时再做增加操作

貌似很简单，但是确实要对栈很熟悉才能想出来，膜拜大佬，我继续努力。

**代码:**
javascript
``` javascript
/*
 * @lc app=leetcode.cn id=1381 lang=javascript
 *
 * [1381] 设计一个支持增量操作的栈
 */

// @lc code=start
/**
 * @param {number} maxSize
 */
var CustomStack = function(maxSize) {
  this.maxSize = maxSize;
  this.satck = []
  this.hash = {}
  this.size = 0
};

/** 
 * @param {number} x
 * @return {void}
 */
CustomStack.prototype.push = function(x) {
  if (this.size<this.maxSize) {
    this.satck.push(x)
    this.size++
  }
};

/**
 * @return {number}
 */
CustomStack.prototype.pop = function() {
  if (this.size=0) return -1
  const top = this.size - 1
  const addVal = this.hash[top]||0
  let item = this.satck.pop();
  this.size-- 
  item+=addVal
  // 这里要注意，如果弹出了值，就证明首位已经加过了
  // 新加进来的数字不需要加，但是他后面的数字还没加
  // 所以首位变为0，下一位加上
  const nowTop = top - 1;
  if (nowTop in this.hash) this.hash[nowTop] += addVal;
  else this.hash[nowTop] = addVal
  this.hash[top] = 0;
  return item
};

/** 
 * @param {number} k 
 * @param {number} val
 * @return {void}
 */
CustomStack.prototype.increment = function(k, val) {
  const index = k>this.size?this.size-1:k-1
  if (index in this.hash) this.hash[index] += val;
  else this.hash[index] = val
};
```

**复杂度分析:**
时间复杂度：最好情况O(1)
空间复杂度：O(n)

**模板：** 无 
