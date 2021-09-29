### 剑指 Offer 47. 礼物的最大价值

#### 描述

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```


#### 提示
```md
1. 0 < grid.length <= 200

2. 0 < grid[0].length <= 200
```

### 解答

+ 解答 1
```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxValue = function(grid) {
    const arr = Array.from(grid, item => Array.from(item)), m = grid.length, n = grid[0].length;

    for(let i = 1; i < n; i++) {
        arr[0][i] += arr[0][i - 1];
    }
    for(let i = 1; i < m; i++) {
        arr[i][0] += arr[i - 1][0];
    }

    for(let i = 1; i < m; i++) {
        for(let j = 1; j < n; j++) {
            arr[i][j] += Math.max(arr[i - 1][j], arr[i][j - 1]);
        }
    }
    return arr[m - 1][n - 1];
};
// 或者
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxValue = function(grid) {
    const m = grid.length, n = grid[0].length, arr = Array(m + 1).fill(0).map(item => Array(n + 1).fill(0));

    for(let i = 1; i <= m; i++) {
        for(let j = 1; j <= n; j++) {
            arr[i][j] = Math.max(arr[i - 1][j], arr[i][j - 1]) + grid[i - 1][j - 1];
        }
    }
    return arr[m][n];
};
```

#### Thoughts

+ 1、经典的动态规划二维数组题。由于是从左上角到右下角，且每次只能向右或者向下，于是构建一个同构的二维数组，第一行的每个位置都只能从左边位置走一步到达，第一列的每个位置只能由上一个位置走一步到达，故先更新这两个数据。接着余下的每个位置，都由上一个位置或者左一个位置更新而来，取其中最大值即可。最后返回右下角的位置的计算结果。

  看了评论还可以多构建一行和一列，然后就不需要提前更新第一行第一列的数据，根据上一个位置和左一个位置的最大值加上当前位置对应的棋盘的值更新即可。