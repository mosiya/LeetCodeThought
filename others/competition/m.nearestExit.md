### 5793. 迷宫中离入口最近的出口

#### 描述

给你一个 m x n 的迷宫矩阵 maze （下标从 0 开始），矩阵中有空格子（用 '.' 表示）和墙（用 '+' 表示）。同时给你迷宫的入口 entrance ，用 entrance = [entrancerow, entrancecol] 表示你一开始所在格子的行和列。

每一步操作，你可以往 上，下，左 或者 右 移动一个格子。你不能进入墙所在的格子，你也不能离开迷宫。你的目标是找到离 entrance 最近 的出口。出口 的含义是 maze 边界 上的 空格子。entrance 格子 不算 出口。

请你返回从 entrance 到最近出口的最短路径的 步数 ，如果不存在这样的路径，请你返回 -1 。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/nearest-exit-from-entrance-in-maze

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:

![](https://assets.leetcode.com/uploads/2021/06/04/nearest1-grid.jpg)
```md
输入：maze = [["+","+",".","+"],[".",".",".","+"],["+","+","+","."]], entrance = [1,2]

输出：1

解释：总共有 3 个出口，分别位于 (1,0)，(0,2) 和 (2,3) 。
一开始，你在入口格子 (1,2) 处。
- 你可以往左移动 2 步到达 (1,0) 。
- 你可以往上移动 1 步到达 (0,2) 。
从入口处没法到达 (2,3) 。
所以，最近的出口是 (0,2) ，距离为 1 步。
```
+ 示例 2:

![](https://assets.leetcode.com/uploads/2021/06/04/nearesr2-grid.jpg)
```md
输入：maze = [["+","+","+"],[".",".","."],["+","+","+"]], entrance = [1,0]

输出：2

解释：迷宫中只有 1 个出口，在 (1,2) 处。
(1,0) 不算出口，因为它是入口格子。
初始时，你在入口与格子 (1,0) 处。
- 你可以往右移动 2 步到达 (1,2) 处。
所以，最近的出口为 (1,2) ，距离为 2 步。
```
+ 示例 3:

![](https://assets.leetcode.com/uploads/2021/06/04/nearest3-grid.jpg)
```md
输入：maze = [[".","+"]], entrance = [0,0]

输出：-1

解释：这个迷宫中没有出口。
```


#### 提示
```md
1. maze.length == m

2. maze[i].length == n

3. 1 <= m, n <= 100

4. maze[i][j] 要么是 '.' ，要么是 '+' 。

5. entrance.length == 2

6. 0 <= entrancerow < m

7. 0 <= entrancecol < n

8. entrance 一定是空格子。
```

### 解答

+ 解答 1
```js
/**
 * @param {character[][]} maze
 * @param {number[]} entrance
 * @return {number}
 */
var nearestExit = function(maze, entrance) {
    const map = Array.from(maze, item => new Array(item.length).fill(Math.min())),
        m = maze.length,
        n = maze[0].length,
        stack = []
        dirs = [[-1, 0], [1, 0], [0, -1], [0, 1]];
    let path = 0;
    stack.push(entrance);
    maze[entrance[0]][entrance[1]] = '+';
    while(stack.length) {
        let len = stack.length;
        while(len) {
            let node = stack.shift();
            const [x, y] = node;
            map[x][y] = path;
            for(let i = 0; i < 4; i++) {
                const [_x, _y] = dirs[i];
                if(x+_x >= 0 && x+_x < m && y+_y >= 0 && y+_y < n && maze[x+_x][y+_y] != '+') {
                    if(x+_x == 0 || x+_x == m - 1 || y+_y == 0 || y+_y == n - 1) {
                        return path + 1;
                    }
                    maze[x+_x][y+_y] = '+';
                    stack.push([x+_x, y+_y]);
                }
            }
            len--;
        }
        path++;
    }
    return -1;
};
```


#### Thoughts

+ 1、感觉这道题是二叉树层序遍历的进阶版。首先要使用一个 m x n 的地图去保存每个位置的步数，然后从起点出发，根据广度遍历，给每个位置赋值步数。当到达边界而该位置没有障碍物时返回步数。为了防止位置赋值时陷入死循环，每次赋值完毕后要将当前位置设置为障碍物即可。

  这道题是竞赛题，当时费了老劲没做出来，现在想想，能想到用地图记录步数，用广度遍历的方法去做，如果思路有了其实不难。