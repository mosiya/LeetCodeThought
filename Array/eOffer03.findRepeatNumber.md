### 剑指 Offer 03. 数组中重复的数字

#### 描述

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：

[2, 3, 1, 0, 2, 5, 3]

输出：2 或 3 
```


#### 提示
```md
2 <= n <= 100000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
    let len = nums.length, arr = [];
    for(let i = 0; i < len; i++) {
        if(arr[nums[i]]) {
            return nums[i];
        } else {
            arr[nums[i]] = true;
        }
    }
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
    let len = nums.length, arr = nums.sort((a, b) => a - b);
    for(let i = 0; i < len - 1; i++) {
        if(arr[i] === arr[i + 1]) {
            return nums[i];
        }
    }
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
    let len = nums.length, arr = nums.map(item => item + 1);
    for(let i = 0; i < len; i++) {
        let index = Math.abs(arr[i]) - 1;
        if(arr[index] < 0)
            return index;

        arr[index] *= -1;
    }
};
```

#### Thoughts

+ 1、判断重复以及数字在0~n之间是否有重复的题已经做了很多了。这题因为重复的数字和个人不限，所以直接上哈希表，这里使用了数组做哈希表，当遇到第一个哈希表已经存在的元素时则返回。

+ 2、还有就是排序，当相邻的元素有相等的时候立刻返回该元素即可。

+ 3、还有就是使用负号进行标记的方法。但因为元素有可能为0，标负数判断不出来，所以先进行了一轮加1的操作，然后再进行负数标记并判断是否已经有负数存在了，有则返回该元素的下标即可。这里要注意的是，取下标需要取绝对值并减1才是真实的下标。