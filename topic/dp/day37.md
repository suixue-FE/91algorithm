# 第三十七天
## 题目描述
动态规划系列（07. 高频面试题 ）

题目描述
70. 爬楼梯
62. 不同路径
121. 买卖股票的最佳时机
122. 买卖股票的最佳时机 II
123. 买卖股票的最佳时机 III
188. 买卖股票的最佳时机 IV
309. 最佳买卖股票时机含冷冻期
714. 买卖股票的最佳时机含手续费

注意事项
高频系列的题目不要求大家全部做完，做你自己觉得有代表性的题目就好，毕竟不是人人都是西法，可以一秒5连鞭
如果碰到不会的题型，比如动态规划，后面会有专题进行讲解的，可以先标记一下，后面学了专题再回来解题
[前往答题](https://github.com/lisansang/91algorithm/issues/63)

## 个人解答

**思路:**

1. 拿一个东西存储值
2. 设定边界值
3. 向下推进

**代码:**

javascript
``` javascript
/*
 * [62] 不同路径
 */

/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function(m, n) {
  let array =[]
  for (let i = 0; i < m; i++) {
    array.push(new Array(n).fill(1))
  }
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (i==0&&j>0) {
        array[i][j] = 1
      }else if (j==0&&i>0) {
        array[i][j] = 1
      }else if(i>0&&j>0){
        array[i][j] = array[i-1][j]+array[i][j-1]
      }
    }
  }
  return array[m-1][n-1]
};
```

**复杂度分析:**
时间复杂度：O(m*n)
空间复杂度：O(m*n)

**代码2:**

javascript
``` javascript
/*
 * @lc app=leetcode.cn id=70 lang=javascript
 *
 * [70] 爬楼梯
 */

// @lc code=start
/**
 * @param {number} n
 * @return {number}
 */

var climbStairs = function(n) {
  const dp = [];
  dp[0] = 1;
  dp[1] = 1;
  for(let i = 2; i <= n; i++) {
      dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n];
};
```

**复杂度分析2:**
时间复杂度：O(n)
空间复杂度：O(n)


**模板：** 
```javascript
var dp = function(m, n) {
  let dp =[]
  for (let i = 0; i < m; i++) {
    dp.push(new Array(n).fill(0))
  }
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      dp[i][j] = dp[i-1][j]+ dp[i][j-1]
    }
  }
  return dp[m-1][n-1]
};
```