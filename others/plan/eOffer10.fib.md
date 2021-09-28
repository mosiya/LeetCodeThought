### 剑指 Offer 10- I. 斐波那契数列

#### 描述

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：
```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：n = 2

输出：1
```
+ 示例 2:
```md
输入：n = 5

输出：5
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
var fib = function(n) {
    let a = 0, b = 1;
    while(n-- > 0) {
        [a, b] = [b, (a + b) % (1e9 + 7)];
    }
    return a % (1e9 + 7);
};
```

+ 解答2
```js
/**
 * @param {number} n
 * @return {number}
 */
var fib = function(n) {
    if(n < 2) return n;
    function multiply(a, b) {
        const res = Array(2).fill(0).map(item => Array(2).fill(0));
        for(let i = 0; i < 2; i++) {
            for(let j = 0; j < 2; j++) {
                res[i][j] = (BigInt(a[i][0]) * BigInt(b[0][j]) + BigInt(a[i][1]) * BigInt(b[1][j])) % BigInt(1e9 + 7);
            }
        }
        return res;
    }
    let prod = [[1, 0], [0, 1]], // 此处的prod为单位矩阵，相当于快速幂里的1
        x = [[1, 1], [1, 0]];
    n--; // 由于得到的prod[0][0]是F(n+1)，要求F(n)，故这里需要自减
    // 以下是快速幂的正统做法
    while(n > 0) {
        if(n & 1) prod = multiply(prod, x);
        x = multiply(x, x);
        n >>= 1;
    }
    return prod[0][0];
};
```


#### Thoughts

+ 1、老生常谈的一道题了。用两个变量来回倒数据，就可以得到答案啦。要注意的就是最后返回的结果是a还是b，可以自己用前几个数据验证一下即可。

+ 2、根据官解，可以构建一个递推关系如下：
  
  $$\left[ \begin{matrix} 1 & 1 \\ 1 & 0 \end{matrix} \right] \left[ \begin{matrix} F(n) \\ F(n - 1) \end{matrix} \right] = \left[ \begin{matrix} F(n) + F(n - 1) \\ F(n) \end{matrix} \right] = \left[ \begin{matrix} F(n+1) \\ F(n) \end{matrix} \right]$$ 

  故有：

  $$\left[ \begin{matrix} F(n+1) \\ F(n) \end{matrix} \right] = \left[ \begin{matrix} 1 & 1 \\ 1 & 0 \end{matrix} \right]^n \left[ \begin{matrix} F(1) \\ F(0) \end{matrix} \right]$$ 

  令：
  
  $$M = \left[ \begin{matrix} 1 & 1 \\ 1 & 0 \end{matrix} \right]$$

  因此只要能快速计算矩阵M的n次幂，就可以得到F(n)的值。可以定义矩阵乘法，然后使用快速幂算法来加速 M^n 的求值。计算的过程中，答案需要模1e9+7