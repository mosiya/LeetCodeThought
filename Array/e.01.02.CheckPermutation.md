### 面试题 01.02. 判定是否互为字符重排

#### 描述

给定两个字符串 s1 和 s2，请编写一个程序，确定其中一个字符串的字符重新排列后，能否变成另一个字符串。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/check-permutation-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: s1 = "abc", s2 = "bca"

输出: true 
```
+ 示例 2:
```md
输入: s1 = "abc", s2 = "bad"

输出: false
```


#### 提示
```md
1. 0 <= len(s1) <= 100

2. 0 <= len(s2) <= 100
```

### 解答

+ 解答 1
```js
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, arr1 = s1.split(''), arr2 = s2.split('');
    for(let i = 0; i < len; i++) {
        let index = arr2.indexOf(arr1[i]);
        if(index > -1) {
            arr2.splice(index, 1);
        } else {
            return false;
        }
    }
    return true;
};
// 或者
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, arr1 = s1.split(''), arr2 = s2.split('');
    for(let i = 0; i < len; i++) {
        let index = arr2.indexOf(arr1[i]);
        if(index === -1) {
            return false;
        }
        arr2[index] = '';
    }
    return true;
};
```

+ 解答 2
```js
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, arr1 = s1.split(''), arr2 = s2.split(''), obj = {};
    for(let i = 0; i < len; i++) {
        if(!obj[arr1[i]]) {
            obj[arr1[i]] = 1;
        } else {
            obj[arr1[i]]++;
        }
    }
    for(let i = 0; i < len; i++) {
        if(!obj[arr2[i]]) {
            return false;
        } else {
            obj[arr2[i]]--;
        }
    }
    return true;
};
// 或者
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, obj = {};
    for(let i = 0; i < len; i++) {
        if(!obj[s1[i]]) {
            obj[s1[i]] = 1;
        } else {
            obj[s1[i]]++;
        }
    }
    for(let i = 0; i < len; i++) {
        if(!obj[s2[i]]) {
            return false;
        } else {
            obj[s2[i]]--;
        }
    }
    return true;
};
```

+ 解答 3
```js
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, arr = new Array(26).fill(0);
    for(let i = 0; i < len; i++) {
        arr[s1[i].charCodeAt() - 'a'.charCodeAt()]++;
        arr[s2[i].charCodeAt() - 'a'.charCodeAt()]--;
    }
    return arr.every(item => item === 0);
};
// 或者
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    if(s1.length !== s2.length) return false;
    let len = s1.length, arr = new Array(26).fill(0);
    for(let i = 0; i < len; i++) {
        arr[s1[i].charCodeAt() - 'a'.charCodeAt()]++;
        arr[s2[i].charCodeAt() - 'a'.charCodeAt()]--;
    }
    for(let i = 0; i < 26; i++) {
        if(arr[i] !== 0) return false;
    }
    return true;
};
```

+ 解答 4
```js
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */
var CheckPermutation = function(s1, s2) {
    return s1.split('').sort().join('') === s2.split('').sort().join('');
};
```

#### Thoughts

+ 1、先把两个字符串打成数组，然后遍历一个数组，对每个元素都查找是否存在于另一个数组中，若不存在则直接返回false，如果存在就从中删掉(保证重复的不会再被检测)，或者设置为空。最后没有返回false，则看这个数组的长度是否为0，为0返回true。

  也可以先判断两个字符串是否相等，不相等返回false，相等再进行遍历，最后通过检测未返回false则返回true。

+ 2、也可以使用哈希表来存储字符串，对其中一个字符串先存一遍所有字符，再对另一个字符串进行字符消除，若出现字符不存在的情况则返回false，最后返回true。当然前提是先判断两个字符串长度是否相等，相等才进行操作。

+ 3、看了解答，可以使用一个数组来当哈希表，并且用字符与a的charCode值之差作为索引来存储。并且存s1一次就减s2一次，最后判断哈希表里的所有元素是否均为0，是则返回true，否则返回false。

+ 4、看了通过的解法，居然还可以先打成数组排序再转成字符串进行比较，执行耗时居然还是最少的。这里就记录一下了，虽然我用这个方法并没有比其他的快。

+ ps：这道题值得小小纪念一下，也许是因为这道题太简单了，所以看通过的解法，几乎用的都是第四种，而我使用的第一种和第二种方案竟然都上榜了，感到神奇又开心，哈哈~给我自己一个小小的鼓励和赞美~