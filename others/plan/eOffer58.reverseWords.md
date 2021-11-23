### 剑指 Offer 58 - I. 翻转单词顺序

#### 描述

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

注意：本题与主站 151 题相同：https://leetcode-cn.com/problems/reverse-words-in-a-string/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: "the sky is blue"

输出: "blue is sky the"
```
+ 示例 2:
```md
输入: "  hello world!  "

输出: "world! hello"

解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```
+ 示例 3:
```md
输入: "a good   example"

输出: "example good a"

解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```


#### 提示
```md
1. 无空格字符构成一个单词。

2. 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。

3. 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

### 解答

+ 解答 1
```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    return s.trim().split(/ +/).reverse().join(' ');
};
```


#### Thoughts

+ 1、题目虽然说是有改动但我没发现改动在哪里。总之详细的题解在 151 了，这里只给了最简单的api做法。