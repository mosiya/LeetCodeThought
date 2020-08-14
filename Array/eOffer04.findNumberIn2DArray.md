### 剑指 Offer 04. 二维数组中的查找

注意：本题与主站 240 题相同：https://leetcode-cn.com/problems/search-a-2d-matrix-ii/

#### 描述

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

现有矩阵 matrix 如下：

```md
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = 5，返回 true。

给定 target = 20，返回 false。


#### 提示
```md
1. 0 <= n <= 1000

2. 0 <= m <= 1000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function(matrix, target) {
    if(matrix.length < 1) return false;
    let n = matrix.length, m = matrix[0].length, row = 0, col = m - 1;
    while(row < n && col >= 0) {
        if(matrix[row][col] === target) {
            return true;
        } else if(matrix[row][col] > target) {
            col--;
        } else {
            row++;
        }
    }
    return false;
};
// 或者
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function(matrix, target) {
    if(matrix.length < 1) return false;
    let n = matrix.length, m = matrix[0].length, row = n - 1, col = 0;
    while(row >= 0 && col < m) {
        if(matrix[row][col] === target) {
            return true;
        } else if(matrix[row][col] > target) {
            row--;
        } else {
            col++;
        }
    }
    return false;
};
```

#### Thoughts

+ 1、这道题这么经典，还需要说吗？找左上角或者右下角开始遍历，小于target就往大的方向移，大于target就往小的方向移，等于就返回true，遍历完了还没返回true就返回false。