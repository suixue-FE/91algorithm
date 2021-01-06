# 第六十六题
## 题目描述
在一个 N x N 的坐标方格 grid 中，每一个方格的值 grid[i][j] 表示在位置 (i,j) 的平台高度。

现在开始下雨了。当时间为 t 时，此时雨水导致水池中任意位置的水位为 t 。你可以从一个平台游向四周相邻的任意一个平台，但是前提是此时水位必须同时淹没这两个平台。假定你可以瞬间移动无限距离，也就是默认在方格内部游动是不耗时的。当然，在你游泳的时候你必须待在坐标方格里面。

你从坐标方格的左上平台 (0，0) 出发。最少耗时多久你才能到达坐标方格的右下平台 (N-1, N-1)？
 

示例 1:

输入: [[0,2],[1,3]]
输出: 3
解释:
时间为0时，你位于坐标方格的位置为 (0, 0)。
此时你不能游向任意方向，因为四个相邻方向平台的高度都大于当前时间为 0 时的水位。

等时间到达 3 时，你才可以游向平台 (1, 1). 因为此时的水位是 3，坐标方格中的平台没有比水位 3 更高的，所以你可以游向坐标方格中的任意位置
示例2:

输入: [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]
输出: 16
解释:
0 1 2 3 4
24 23 22 21 5
12 13 14 15 16
11 17 18 19 20
10 9 8 7 6

最终的路线用加粗进行了标记。
我们必须等到时间为 16，此时才能保证平台 (0, 0) 和 (4, 4) 是连通的
 

提示:

2 <= N <= 50.
grid[i][j] 位于区间 [0, ..., N*N - 1] 内。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/swim-in-rising-water
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

## 个人解答

**思路:**

最开始的思路，从grid[0][0]的数字 开始++ ，然后用DFS判断是否能到达对应最后为止。
直到++到能通过为止，返回能通过的第一个数字。

改进思路，grid中取最大值和grid[0][0]作为二分边界，能通过 最大值 = t,不能通过则最小值=t+1

（前面弄了一个小时，后面弄了半个小时，一道题搞了一个半小时。。。）

**代码:**
javascript
``` javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var swimInWater = function(grid) {
    const n = grid.length-1
    let maxVal = 0
    let minVal = grid[0][0]-1
    for(let i =0;i<=n;i++){
        for(let j =0;j<=n;j++){
        const max = grid[i][j]
        maxVal = max>maxVal?max:maxVal
      }
    }
    function goNext(x,y,resTest){
        const value = grid[x][y]
        if(value<=resTest){
            arr[x][y] = 1
            if(x===n&&y===n){
                return
            }else{
                if(x<n&&arr[x+1][y]===0)goNext(x+1,y,resTest)
                if(y<n&&arr[x][y+1]===0)goNext(x,y+1,resTest) 
                if(x>0&&arr[x-1][y]===0)goNext(x-1,y,resTest)
                if(y>0&&arr[x][y-1]===0)goNext(x,y-1,resTest)
            }
        }else{
            arr[x][y] = 0
        }
    }
    
    while (minVal<maxVal) {
        const t = (maxVal+minVal)>>1
        let arr = new Array(n+1).fill(0).map(item => {
            return new Array(n+1).fill(0)
        })
        goNext(0, 0, t)
        if(arr[n][n]===1) maxVal = t
        else minVal = t+1
    }
    return maxVal
};
```

**复杂度分析:**
时间复杂度O(n*n*logMax)
空间复杂度O(n*n)
 
**模板**
dfs模板+二分