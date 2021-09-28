### 剑指 Offer 58 - II. 左旋转字符串

#### 描述

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: s = "abcdefg", k = 2

输出: "cdefgab"
```
+ 示例 2:
```md
输入: s = "lrloseumgh", k = 6

输出: "umghlrlose"
```


#### 提示
```md
1 <= k < s.length <= 10000
```

### 解答

+ 解答 1
```js
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
var reverseLeftWords = function(s, n) {
    return s.substring(n) + s.substring(0, n);
};
```

+ 解答 2
```js
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
var reverseLeftWords = function(s, n) {
    let res = '';
    for(let i = n; i < n + s.length; i++) {
        res += s.charAt(i % s.length);
    }
    return res;
};
```


#### Thoughts

+ 1、直接使用字符串的api，切分n后部分和前面部分然后拼接起来即可。

+ 2、从字符串n的位置开始，对字符串的长度取余，得到整个字符串的结果。