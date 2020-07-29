### 面试题 17.10. 主要元素

#### 描述

数组中占比超过一半的元素称之为主要元素。给定一个整数数组，找到它的主要元素。若没有，返回-1。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/find-majority-element-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：[1,2,5,9,5,9,5,5,5]

输出：5
```
+ 示例 2:
```md
输入：[3,2]

输出：-1
```
+ 示例 3:
```md
输入：[2,2,1,1,1,2,2]

输出：2
```

#### 进阶
```md
你有办法在时间复杂度为 O(N)，空间复杂度为 O(1) 内完成吗？
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let obj = {}, max = 0, res = -1, len = nums.length >> 1;
    for(let num of  nums) {
        if(!obj[num]) obj[num] = 0;
        obj[num]++;
    }
    max = Math.max(...Object.values(obj));
    if(max > len) return Object.entries(obj).filter(item => item[1] = max)[0][0];
    return -1;
};
// 或者
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let obj = {}, max = 0, res = -1, len = nums.length >> 1;
    for(let num of  nums) {
        if(!obj[num]) obj[num] = 0;
        obj[num]++;
        if(obj[num] > max) {
            max = obj[num];
            if(obj[num] > len) return num;
        }
    }
    return -1;
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let len = nums.length;
    while(nums.length) {
        let num = nums[0];
        nums = nums.filter(item => item != num);
        let remove = len - nums.length;
        if(remove > len >> 1) {
            return num;
        }
    }
    return -1;
};
// 或者
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let len = nums.length, halfLen = len >> 1;
    while(nums.length > halfLen) {
        let num = nums[0];
        nums = nums.filter(item => item != num);
        let remove = len - nums.length;
        if(remove > halfLen) {
            return num;
        }
    }
    return -1;
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let major = nums[0], count = 0, c = 0;
    for(let num of nums) {
        if(major !== num) {
            if(count === 0) {
                major = num;
                count++;
            } else {
                count--;
            }
        } else {
            count++
        }
    }
    for(let num of nums) {
        if(num === major) {
            c++
        }
    }
    if(c <= nums.length >> 1) return -1;
    return major;
};
```

+ 解答 4
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let major = 0, count = 0, len = nums.length >> 1;
    for(let i = 0; i < 32; i++) {
        count = 0;
        bit = 1 << i;
        for(let num of nums) {
            if(num & bit) count++;
        }
        if(count > len) major ^= bit
    }
    return nums.indexOf(major) > -1 ? major : -1;
};
```

#### Thoughts

+ 1、这是一道看似简单的题，做起来也很套路，哈希表存元素并统计频次，找到频次最高那个判断是否大于数组长度的一半即可。复杂做法做了一遍，又优化了一下。

+ 2、后来想到一种做法，是对当前的nums每次都去掉与第一个元素相同的元素，然后统计被移除的元素个数，遇到超过数组长度一半的就返回，否则返回-1。
  
  优化的做法是把while循环里的判断改成nums.length > halfLen，可以提前退出循环。

+ 3、这道题本来应该昨天就解决了的，但是看了解答发现，原来有一种更简单直接的做法，也就是题目里进阶的要求，时间复杂度仍然为O(n)，但空间复杂度要求降到O(1)。

  这里就要介绍一种技巧性很强、专门解决大半数元素这一类问题的解法了——摩尔投票法。

  摩尔投票法的思路是，若当前数组必定存在一个元素，它出现的频次超过半数，那么只要进行投票，遇到它时加1，否则减1，则最后必定会出现投票数大于0的情况，而找到的这个元素就是出现频次超过半数的元素了。

  具体做法就是，使用两个变量，major记录当前元素，count统计频次。遍历整个数组，遇到当前元素时，若与major记录的元素一致，则count++；若不一致时，判断count是否为0，若不为0，则count--，否则将major替换为当前元素，并记录count++。

  而摩尔投票成立的前提是数组内必定存在频次超过半数的元素。对于本题，还需要考虑若不存在这样的数组时，如何修正结果？

  修正的做法就是再进行一次验证：当找到这样的major时，再对整个数组遍历一次统计major出现的频次，若频次超过半数则返回major，否则返回-1。

  这个做法非常巧妙，技巧性和针对性很强，以后再遇到类似的题都可以使用这种做法。

+ 4、还有一种技巧性很强的做法，而且更不容易想到，就是利用二进制数值进行判断出现频次超过一半的元素。

  这种做法的原理就是：对于这个数组来说，如果有一个元素的频次大于半数，那么这个元素的二进制数值的频次也大于半数。
  
  那么可以这样做：设置一个为0的major作为最后的结果（它的32个比特位都为0）。对数组的每一个元素的32个比特位进行一一的位运算。若某一个比特位上的1大于半数，则把major对应的比特位设置为1。

  这样组装出来的major，如果存在于原数组中，说明这个元素就是要找的元素，否则返回-1。

  这样的做法理解以后就不难了，难的是一开始接触的时候看代码，太费神了，所以昨天最后没弄完，需要一点时间进行消化。