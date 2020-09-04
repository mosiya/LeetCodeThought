### 面试题 17.04. 消失的数字

#### 描述

数组nums包含从0到n的所有整数，但其中缺了一个。请编写代码找出那个缺失的整数。你有办法在O(n)时间内完成吗？

注意：本题相对书上原题稍作改动

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/missing-number-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：[3,0,1]

输出：2
```
+ 示例 2:
```md
输入：[9,6,4,2,3,5,7,0,1]

输出：8
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    let sum1 = nums.reduce((a, b) => a + b), len = nums.length, sum2 = (1 + len) * len / 2;
    return sum2 - sum1;
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    let arr = nums.sort((a, b) => a - b), len = nums.length;
    for(let i = 0; i < len; i++) {
        if(arr[i] !== i) {
            return i;
        }
    }
    return len;
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    let len = nums.length + 1, sum = 0;
    nums.push(0);
    for(let i = 0; i < len; i++) {
        sum += i - nums[i];
    }
    return sum;
};
// 或者
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingNumber = function(nums) {
    let len = nums.length, res = 0;
    for(let i = 0; i < len; i++) {
        res ^= i ^ nums[i];
    }
    return res ^ len;
};
```

#### Thoughts

+ 1、这道题好像做了好几次了，因为缺失的就一个数，故加和相减是最容易想到的。这里要注意的是从0开始的，所以如果按0到n的加和，长度应该是n+1，也可以从1加到n，长度为n来计算。

+ 2、还有就是排序然后看下标与元素是否一致，第一个不一致的就是缺失的元素，都一致说明缺失的是最后一个元素，与数组长度相等。

+ 3、还有就是用下标与元素相减，也可以用异或的方法，异或会将相等的元素和下标抵消掉，和相减的效果是一样的。相减的需要加入n，异或也需要与n异或一次。