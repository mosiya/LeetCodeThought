### 剑指 Offer 50. 第一个只出现一次的字符

#### 描述

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：s = "abaccdeff"

输出：'b'
```
+ 示例 2:
```md
输入：s = "" 

输出：' '
```


#### 提示
```md
0 <= s 的长度 <= 50000
```

### 解答

+ 解答 1
```js
/**
 * @param {string} s
 * @return {character}
 */
var firstUniqChar = function(s) {
    const map = new Map();
    for(let string of s) {
        map.set(string, (map.get(string) || 0) + 1);
    }
    for(const item of map) {
        if(item[1] == 1) {
            return item[0];
        }
    }
    return ' ';
};
```

+ 解答 2
```js
/**
 * @param {string} s
 * @return {character}
 */
var firstUniqChar = function(s) {
    const obj = new Object, queue = [];
    for(let [i, ch] of Array.from(s).entries()) {
        if(!(ch in obj)) {
            obj[ch] = i;
            queue.push(ch);
        } else {
            obj[ch] = -1;
            while(queue.length && obj[queue[0]] === -1) {
                queue.shift();
            }
        }
    }
    return queue.length ? queue[0] : ' ';
};
```


#### Thoughts

+ 1、利用map的性质，map会根据存储的顺序不断更新迭代的顺序，所以只要遍历一次字符串存储频次，然后再遍历map，找到的第一个频次为1的就是第一个频次为1的字符。

+ 2、如果哈希表是无序的，那么就需要使用一个队列来存储顺序了。具体做法就是当字符第一次哈希存储的时候，同时入队；当出现重复的字符时，把出现在队头的重复字符出队。这里之所以用while，是因为可能重复的字符不在队头，而当队头的字符变成重复字符的时候，它的后面的字符也可能是之前重复过但没有出队的，所以要一直出队直到让第一个非重复字符来到队头，或者队空为止。最后看队列是否为空返回结果