### 剑指 Offer 10- II. 青蛙跳台阶问题

#### 描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

注意：本题与主站 70 题相同：https://leetcode-cn.com/problems/climbing-stairs/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：n = 2

输出：2
```
+ 示例 2:
```md
输入：n = 7

输出：21
```
+ 示例 3:
```md
输入：n = 0

输出：1
```


#### 提示
```md
0 <= n <= 100
```

### 解答

+ 解答 1
```js
/**
 * @param {number} n
 * @return {number}
 */
var numWays = function(n) {
    let a = 1, b = 1;
    while(n-- > 0) {
        [a, b] = [b, (a + b) % (1e9 + 7)];
    }
    return a;
};
```


#### Thoughts

+ 1、斐波那契数列的青蛙跳台题，设跳到 n 级台阶的方法有f(n)种，由于青蛙每次只能跳1级和2级，所以最后一跳，青蛙可能从 n-1 级起跳，也可以从 n-2 级起跳。故f(n)= f(n-1) + f(n-2)。而f(0) = 1，f(1) = 1，于是可以写代码如上。

+ 快速幂的方法参考 剑指 Offer 10- I. 斐波那契数列，这里不再赘述