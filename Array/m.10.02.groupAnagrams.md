### 面试题 10.02. 变位词组

#### 描述

编写一种方法，对字符串数组进行排序，将所有变位词组合在一起。变位词是指字母相同，但排列不同的字符串。

注意：本题相对原题稍作修改

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/group-anagrams-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```


#### 提示
```md
1. 所有输入均为小写字母。

2. 不考虑答案输出的顺序。
```

### 解答

+ 解答 1
```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
    let map = new Map();
    for(let s of strs) {
        const string = s.split('').sort().join('');
        map.get(string) ? map.get(string).push(s) : map.set(string, [s]);
    }
    return [...map.values()];
};
```

+ 解答 2
```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function(strs) {
    let map = new Map();
    for(let str of strs) {
        const array = new Array(26).fill(0);
        for(let s of str) {
            array[s.charCodeAt() - 'a'.charCodeAt()]++;
        }
        const string = array.join('');
        map.has(string) ? map.get(string).push(str) : map.set(string, [str]);
    }
    return [...map.values()];
};
```


#### Thoughts

+ 1、既然是相同字母组成的不同排序的字符串，那么只要使用哈希表来存储对应的相同字母下的变位词组即可。为了保证哈希表的key的一致性，需要对字母进行排序，然后就保存数组即可。最后输出哈希表的值构成的数组。

+ 2、方法2没有大的区别，主要是将字符串排序改为计数排序，然后得到唯一的key值作为哈希表的键，其他的做法都一样。