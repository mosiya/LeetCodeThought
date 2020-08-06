### 面试题 16.04. 井字游戏

#### 描述

设计一个算法，判断玩家是否赢了井字游戏。输入是一个 N x N 的数组棋盘，由字符" "，"X"和"O"组成，其中字符" "代表一个空位。

以下是井字游戏的规则：

玩家轮流将字符放入空位（" "）中。
第一个玩家总是放字符"O"，且第二个玩家总是放字符"X"。
"X"和"O"只允许放置在空位中，不允许对已放有字符的位置进行填充。
当有N个相同（且非空）的字符填充任何行、列或对角线时，游戏结束，对应该字符的玩家获胜。
当所有位置非空时，也算为游戏结束。
如果游戏结束，玩家不允许再放置字符。
如果游戏存在获胜者，就返回该游戏的获胜者使用的字符（"X"或"O"）；如果游戏以平局结束，则返回 "Draw"；如果仍会有行动（游戏未结束），则返回 "Pending"。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/tic-tac-toe-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入： board = ["O X"," XO","X O"]

输出： "X"
```
+ 示例 2:
```md
输入： board = ["OOX","XXO","OXO"]

输出： "Draw"

解释： 没有玩家获胜且不存在空位
```
+ 示例 3:
```md
输入： board = ["OOX","XXO","OX "]

输出： "Pending"

解释： 没有玩家获胜且仍存在空位
```


#### 提示
```md
1. 1 <= board.length == board[i].length <= 100

2. 输入一定遵循井字棋规则
```

### 解答

+ 解答 1
```js
/**
 * @param {string[]} board
 * @return {string}
 */
var tictactoe = function(board) {
    let n = board.length, isPending = false, flag, chess;
    for(let i = 0; i < n; i++) { // 行
        flag = true;
        chess = board[i][0];
        if(chess === ' ') {
            isPending = true;
            continue;
        }
        for(let c of board[i]) {
            if(c !== chess) {
                flag = false;
                break;
            }
        }
        if(flag) return chess;
    }

    for(let j = 0; j < n; j++) { // 列
        flag = true;
        chess = board[0][j];
        if(chess === ' ') {
            isPending = true;
            continue;
        }
        for(let i = 0; i < n; i++) {
            if(board[i][j] !== chess) {
                flag = false;
                break;
            }
        }
        if(flag) return chess;
    }

    flag = true;
    chess = board[0][0];
    for(let i = 0; i < n; i++) { // 对角线
        let c = board[i][i];
        if(c === ' ') {
            isPending = true;
            flag = false;
            break;
        } else if(c !== chess) {
            flag = false;
            break;
        }
    }
    if(flag) return chess;

    flag = true;
    chess = board[0][n - 1];
    for(let i = 0; i < n; i++) { // 对角线
        let c = board[i][n - 1 - i];
        if(c === ' ') {
            isPending = true;
            flag = false;
            break;
        } else if(c !== chess) {
            flag = false;
            break;
        }
    }
    if(flag) return chess;

    return isPending ? 'Pending' : 'Draw';
};
```


#### Thoughts

+ 1、我觉得我写得中规中矩吧，四段循环分别进行 行、列、对角线的判断，对称的判断也写得很对称，个人觉得还是比较满意的。具体要想清楚有几种情况，我的分析是，先判断是否有获胜的情况，再判断是否已经落子结束。

  在每次遍历时，都要判断一下是否存在空位置，存在则说明落子未结束。

  于是开始遍历判断是否胜出。我使用的做法是用一个开关和一个棋子去记录是否有获胜的情况和当前的棋子是什么。

  行遍历就只取每行第一个元素进行后续判断，而且后续判断也要从0开始，因为还需要判断是否为空的情况；

  列遍历就只取第一列的每个元素进行后续判断；

  对角线就简单些，取第一行第一个和最后一个分别进行后续判断即可。

  其他都是细节问题了。出错过的原因有，行列遍历的时候需要在二层循环之前每次都重置flag开关；以及判断是否为空字符串时应该有一个空格，而不是真的空字符串。

  然后就通过啦。

  看了解答还有将元素拼接起来再进行判断的，还有用正则来判断的，因为代码都太长了，我决定保留我自己的写法不再改动了。就酱。