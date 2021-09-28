### 剑指 Offer 05. 替换空格

#### 描述

请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：s = "We are happy."

输出："We%20are%20happy."
```


#### 提示
```md
0 <= s 的长度 <= 10000
```

### 解答

+ 解答 1
```js
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
    return s.replace(/ /g, '%20');
};
```

+ 解答 2
```js
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
    return s.split(' ').join('%20')
};
```


#### Thoughts

+ 1、全局替换空格为%20即可，很简单。

+ 2、将字符串以空格切分为数组，再用%20拼接起来即可。