### 1160. 拼写单词

#### 描述

给你一份『词汇表』（字符串数组） words 和一张『字母表』（字符串） chars。

假如你可以用 chars 中的『字母』（字符）拼写出 words 中的某个『单词』（字符串），那么我们就认为你掌握了这个单词。

注意：每次拼写（指拼写词汇表中的一个单词）时，chars 中的每个字母都只能用一次。

返回词汇表 words 中你掌握的所有单词的 长度之和。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：words = ["cat","bt","hat","tree"], chars = "atach"

输出：6

解释： 

可以形成字符串 "cat" 和 "hat"，所以答案是 3 + 3 = 6。
```
+ 示例 2:
```md
输入：words = ["hello","world","leetcode"], chars = "welldonehoneyr"

输出：10

解释：

可以形成字符串 "hello" 和 "world"，所以答案是 5 + 5 = 10。
```


#### 提示：
```md
1. 1 <= words.length <= 1000

2. 1 <= words[i].length, chars.length <= 100

3. 所有字符串中都仅包含小写英文字母
```

### 解答

+ 解答 1
```js
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    return words.filter(item => {
        if(item.length > chars.length) return false;
        let _chars = chars;
        for(let i of item) {
            if(_chars.length < 1) return false;
            let index = _chars.indexOf(i);
            if(index < 0) {
                return false
            } else {
                _chars = _chars.slice(0, index) + _chars.slice(index + 1);
            }
        }
        return true;
    }).reduce((pre, cur) => {
        return pre + cur.length
    }, 0)
};
```

+ 解答 2
```js
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    let charsObj = {};
    for(let c of chars) {
        if(!charsObj[c]) charsObj[c] = 0;
        charsObj[c] ++;
    }
    return words.filter(item => {
        let obj = {};
        for(let i of item) {
            if(!obj[i]) obj[i] = 0;
            obj[i] ++;
        }
        for(let c in obj) {
            if(!charsObj[c] || obj[c] > charsObj[c]) {
                return false
            }
        }
        return true;
    }).reduce((pre, cur) => pre + cur.length, 0)
};
// 或者
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    let len = 0;
    let charsObj = {};
    for(let c of chars) {
        if(!charsObj[c]) charsObj[c] = 0;
        charsObj[c] ++;
    }
    words.forEach(item => {
        let obj = {};
        for(let i of item) {
            if(!obj[i]) obj[i] = 0;
            obj[i] ++;
        }
        let flag = true;
        for(let key in obj) {
            if(!charsObj[key] || obj[key] > charsObj[key]) {
                flag = false;
                break;
            }
        }
        if(flag) len += item.length
    })
    return len;
};
```

+ 解答 3
```js
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    let len = 0;
    let charArr = new Array(26).fill(0);
    for(let c of chars) {
        charArr[c.charCodeAt() - 'a'.charCodeAt()] ++;
    }
    words.forEach(item => {
        let arr = new Array(26).fill(0);
        for(let c of item) {
            arr[c.charCodeAt() - 'a'.charCodeAt()] ++;
        }
        let flag = true;
        for(let i = 0; i < arr.length; i++) {
            if(arr[i] > charArr[i]) {
                flag = false;
                break;
            }
        }
        if(flag) len += item.length
    })
    return len;
};
// 或者
/**
 * @param {string[]} words
 * @param {string} chars
 * @return {number}
 */
var countCharacters = function(words, chars) {
    if(!words || words.length < 1 || !chars) return 0;
    let len = 0;
    let charArr = new Array(26).fill(0);
    for(let c of chars) {
        charArr[c.charCodeAt() - 'a'.charCodeAt()] ++;
    }
    words.forEach(item => {
        let arr = new Array(26).fill(0);
        let flag = true;
        for(let c of item) {
            let key = c.charCodeAt() - 'a'.charCodeAt();
            if(arr[key] ++ === charArr[key]) return false;
        }
        if(flag) len += item.length
    })
    return len;
};
```

#### Thoughts

+ 1、这道题，最直观的做法就是对于words数组里的每一个单词，都把单词的每个字母去chars里进行字母的匹配，并且每匹配中一个字母就剔除一个字母，直到每个字母都可以匹配中，那么这个单词就是可以拼写的。

  然后我使用了一个filter去过滤这些单词，并且通过链式操作，用reduce将过滤出来的单词长度进行相加，最后返回。

  其中，值得注意的点有：

  ①每次进行chars匹配的时候，都使用的是chars的一个副本，因为需要修改该字符串。而剔除字母的操作，我使用的是找到字母匹配到的位置，然后进行位置前后slice再拼接。

  ②reduce进行操作的时候，先用一个初始值0作为开始，接下来的长度相加，是前一个的结果加上当前元素的字符串长度（以前经常在这里翻车，就是因为每次都会把两个都取成长度，搞得很麻烦。其实只要设置一个初始值，然后每次都取当前元素的长度就好，前一个结果直接使用就好）

+ 2、看了解答，说使用哈希表来存储计算chars字符串内每一个字符的个数，然后对words里的每一个单词都进行类似的操作，然后比较两个哈希表中对应字符的个数，用这种方式得到这些单词是否能被chars拼写。

  这是一个不错的方案，于是我埋头开始写解答，结果跑出来的时间是我第一个解答的10倍(捂脸)

  仔细看了看，是因为我在存哈希表的时候，对于每一个字符，都会执行一次哈希表的字符是否存在的判断，并且在比较字符的个数时，用了for...in的操作，可能会将对象的原型属性也带入操作，所以虽然解答通过了，但是时间花得很多。

  而且我很迷恋这种filter完了然后reduce的做法。实际上也可以在每次比较时，就得到该单词是否可以被chars拼写的结果，比较完毕时，就可以将该单词的长度统计到结果中去了。

  不过，这两种做法，时间都非常地久。

+ 3、以前做过一道类似的题，是将key有确定上限长度的哈希表用数组来存储，并且直接初始化。这样就不需要对每个字符都判断一次是否存在了。由于本题的字母均为小写字母，故长度最大为26。其他操作跟2差不多，只是将对象操作换成了数组操作，而时间开销降为了2的十分之一。

  需要注意的点有：

  ①如何将字符为key转化为数字做下标？这里有一个技巧，是将字符的charCode与'a'的charCode进行相减的操作，这样就得到了连续的从0~25的下标。

  ②从答案里耗时最短的解答里可以得到另一个小技巧，可以一次遍历判断得到结果，不需要哈希完再遍历一次进行比较。
  
  主要看最后一段代码的实现，若当前的key对应的个数(未加1)已经与charArr[key]相等，说明加1以后必定不相等，故返回false。这个有点难想，所以作为一个小技巧可以去记忆。