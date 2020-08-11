### 面试题 01.01. 判定字符是否唯一

#### 描述

实现一个算法，确定一个字符串 s 的所有字符是否全都不同。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/is-unique-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: s = "leetcode"

输出: false 
```
+ 示例 2:
```md
输入: s = "abc"

输出: true
```


#### 提示
```md
1. 0 <= len(s) <= 100

2. 如果你不使用额外的数据结构，会很加分。
```

### 解答

+ 解答 1
```js
/**
 * @param {string} astr
 * @return {boolean}
 */
var isUnique = function(astr) {
    let obj = {};
    for(let c of astr) {
        if(!obj[c]) {
            obj[c] = true;
        } else {
            return false;
        }
    }
    return true;
};
```

+ 解答 2
```js
/**
 * @param {string} astr
 * @return {boolean}
 */
var isUnique = function(astr) {
    let arr = astr.split('').sort();
    for(let i = 0; i < arr.length - 1; i++) {
        if(arr[i] === arr[i + 1]) return false;
    }
    return true;
};
```

+ 解答 3
```js
/**
 * @param {string} astr
 * @return {boolean}
 */
var isUnique = function(astr) {
    let mark = 0;
    for(let c of astr) {
        let index = c.charCodeAt() - 'a'.charCodeAt();
        if((mark & 1 << index) === 0) {
            mark |= 1 << index;
        } else {
            return false;
        }
    }
    return true;
};
```

+ 解答 4
```js
/**
 * @param {string} astr
 * @return {boolean}
 */
var isUnique = function(astr) {
    return new Set(astr).size === astr.length;
};
```


#### Thoughts

+ 1、检查重复离不开哈希表，于是就靠这个来判断是否有重复字符串了。

+ 2、提示里有说可以用时间复杂度为O(NlogN)的方法，那就是排序了，所以用排序写了一遍，但是这实际上也算是用了新的数据结构吧，pass。

+ 3、看了答案，用了二进制来存，一个数值，有32位比特，本题其实没有说全是小写字母，只能说姑且可用，毕竟测试用例也全是小写的，所以可以用一个比特位记录该字母是否存在，一共26个字母，使用与a的字符串charCode之差作为位数，就OK了。如果按位与为0，说明不存在该字母，否则返回false，说明有重复。

+ 4、看了JavaScript的解法，还有使用set来去重然后对比长度的，够简单。注意set用的是size求长度。