### 面试题 08.03. 魔术索引

#### 描述

魔术索引。 在数组A[0...n-1]中，有所谓的魔术索引，满足条件A[i] = i。给定一个有序整数数组，编写一种方法找出魔术索引，若有的话，在数组A中找出一个魔术索引，如果没有，则返回-1。若有多个魔术索引，返回索引值最小的一个。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/magic-index-lcci

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：nums = [0, 2, 3, 4, 5]

输出：0

说明: 0下标的元素为0
```
+ 示例 2:
```md
输入：nums = [1, 1, 1]

输出：1
```


#### 提示
```md
1. nums长度在[1, 1000000]之间

2. 此题为原书中的 Follow-up，即数组中可能包含重复元素的版本
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMagicIndex = function(nums) {
    let len = nums.length;
    for(let i = 0; i < len; i++) {
        if(nums[i] === i) {
            return i;
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
var findMagicIndex = function(nums) {
    return _findMagicIndex(nums, 0, nums.length - 1);
};
function _findMagicIndex(nums, left, right) {
    if(left > right) return -1;
    let mid = (left + right) >> 1, leftAnswer = _findMagicIndex(nums, left, mid - 1);
    if(leftAnswer !== -1) {
        return leftAnswer;
    } else if(nums[mid] === mid) {
        return mid;
    }
    return _findMagicIndex(nums, mid + 1, right);
}
// 或者
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMagicIndex = function(nums) {
    function _findMagicIndex(left, right) {
        if(left > right) return -1;
        let mid = (left + right) >> 1, leftAnswer = _findMagicIndex(left, mid - 1);
        if(leftAnswer !== -1) {
            return leftAnswer;
        } else if(nums[mid] === mid) {
            return mid;
        }
        return _findMagicIndex(mid + 1, right);
    }
    return _findMagicIndex(0, nums.length - 1);
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMagicIndex = function(nums) {
    let len = nums.length;
    for(let i = 0; i < len;) {
        if(nums[i] === i) return i;
        i = Math.max(nums[i], ++i);
    }
    return -1;
};
```

#### Thoughts

+ 1、最容易想到也是最好做的方法就是暴力破解，直接遍历，找到第一个下标等于当前元素的 就返回下标，否则最后返回-1。

+ 2、官方题解给出了分治的做法。一说分治又开始怕了，这道题就是类似于二分查找，但由于数组中含有重复元素，所以不能单纯靠判断当前元素与下标的关系就可以直接剪枝。

  仔细分析起来，就只有当下标等于当前元素时，可以知道最小的魔术索引一定不在右边，故可进行剪枝，求左边的魔术索引是否存在，若存在则返回左边的魔术索引，否则返回当前的下标。

  如是进行一番递归操作，可得到最终的答案。

+ 3、还有一种方案其实可以想到的，就是在遍历的时候，每次都取当前元素与下标加1中大的那个作为下一次访问的索引，可以跳跃经过很多元素，加快速度找到魔术索引。