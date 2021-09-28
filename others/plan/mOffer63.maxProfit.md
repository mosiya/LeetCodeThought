### 剑指 Offer 63. 股票的最大利润

#### 描述

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

注意：本题与主站 121 题相同：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: [7,1,5,3,6,4]

输出: 5

解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```
+ 示例 2:
```md
输入: [7,6,4,3,1]

输出: 0

解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```


#### 提示
```md
0 <= 数组长度 <= 10^5
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let min = Math.min(), res = 0;
    for(const price of prices) {
        min = Math.min(min, price);
        res = Math.max(res, price - min);
    }
    return res;
};
```


#### Thoughts

+ 1、动态规划的经典题，在121题有详细的题解。当年的自己也思考了一种方法，每个位置存储左边的最小值和右边的最大值，然后遍历得到相减差值最大的值。用动态规划的思维来说，只要求当前元素左边的最小值和当前元素的差值，求最大值即可。