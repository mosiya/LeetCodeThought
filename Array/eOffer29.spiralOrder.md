### 剑指 Offer 29. 顺时针打印矩阵

注意：本题与主站 54 题相同：https://leetcode-cn.com/problems/spiral-matrix/

#### 描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]

输出：[1,2,3,6,9,8,7,4,5]
```
+ 示例 2:
```md
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]

输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```


#### 提示
```md
1. 0 <= matrix.length <= 100

2. 0 <= matrix[i].length <= 100
```

### 解答

+ 解答 1
```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    if(matrix.length < 1) return [];
    let Rlen = matrix.length, Clen = matrix[0].length, n = Rlen * Clen,
        rStart = 0, cStart = 0, rEnd = Rlen - 1, cEnd = Clen - 1, res = [];

    while(res.length < n) {
        for(let j = cStart; j <= cEnd; j++) {
            res.push(matrix[rStart][j]);
        }
        rStart++;
        if(res.length >= n) break;
        for(let i = rStart; i <= rEnd; i++) {
            res.push(matrix[i][cEnd]);
        }
        cEnd--;
        if(res.length >= n) break;
        for(let j = cEnd; j >= cStart; j--) {
            res.push(matrix[rEnd][j]);
        }
        rEnd--;
        if(res.length >= n) break;
        for(let i = rEnd; i >= rStart; i--) {
            res.push(matrix[i][cStart]);
        }
        cStart++;
    }
    return res;
};
// 或者
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    if(matrix.length < 1) return [];
    let Rlen = matrix.length, Clen = matrix[0].length, n = Rlen * Clen,
        rStart = 0, cStart = 0, rEnd = Rlen - 1, cEnd = Clen - 1, res = [];

    while(cStart <= cEnd && rStart <= rEnd) {
        for(let j = cStart; j <= cEnd; j++) {
            res.push(matrix[rStart][j]);
        }
        rStart++;
        if(rStart > rEnd) break;
        for(let i = rStart; i <= rEnd; i++) {
            res.push(matrix[i][cEnd]);
        }
        cEnd--;
        if(cStart > cEnd) break;
        for(let j = cEnd; j >= cStart; j--) {
            res.push(matrix[rEnd][j]);
        }
        rEnd--;
        if(rStart > rEnd) break;
        for(let i = rEnd; i >= rStart; i--) {
            res.push(matrix[i][cStart]);
        }
        cStart++;
    }
    return res;
};
```

#### Thoughts

这题与力扣主站的第54题一样，54题是中等题，这道题算在简单题里，实在是不对等(捂脸笑哭)

这道题我是见过的，甚至还跟着答案写过一遍代码，还通过过。无奈不是自己想出来的，写过一万遍也没用。昨天就在这道题上停下来了，转头刷了两道中等题再回来，还是无从下手，心里着急得不行，最后还是没做完。

今天的状态也不是很好，上午试着调试了一下，最后修修补补，没想到通过了，还是挺开心的。自己做过以后，再看答案再看自己的，有种很痛快的感觉，我再也不是那个面对算法题一筹莫展的小朋友了。

+ 1、只用了一种方案，就是老老实实地按顺序慢慢做，想清楚了四轮遍历是怎么走的，然后确定终止条件是结果数组长度等于给定二维数组的行数乘以列数，就可以了。

  我在理清楚这些逻辑以后，发现总是会有重复遍历的情况出现，想想还是这四个循环要好好管控一下，在每个循环结束后加一个判断，结果数组是否已经完备，是就跳出整个循环，否则就继续。

  于是就通过了。

  看答案其实跟我的也差不多，也有使用下标来判断循环是否继续的，在我这里，如果这样判断，内循环每个结束后都要判断一下下标的大小，也能通过。就是时间时长时短，很难判断说哪个更好一些。

  我觉得都好。