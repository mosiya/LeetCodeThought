### 剑指 Offer 53 - I. 在排序数组中查找数字 I

#### 描述

统计一个数字在排序数组中出现的次数。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: nums = [5,7,7,8,8,10], target = 8

输出: 2
```
+ 示例 2:
```md
输入: nums = [5,7,7,8,8,10], target = 6

输出: 0
```


#### 限制
```md
0 <= 数组长度 <= 50000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    return nums.indexOf(target) > -1 ? nums.lastIndexOf(target) - nums.indexOf(target) + 1 : 0;
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    return nums.filter(item => item === target).length;
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    let i = 0, j = nums.length - 1;
    while(i <= j) {
        if(nums[i] < target) {
            i++
        } else if(nums[j] > target) {
            j--;
        } else {
            return j - i + 1;
        }
    }
    return 0;
};
// 或者
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    let len = nums.length, i = 0, j = len - 1, count = 0;
    while(i <= j) {
        let mid = (i + j) >> 1;
        if(nums[mid] < target) {
            i = mid + 1;
        } else if ( nums[mid] >= target) {
            j = mid - 1;
        }
    }
    while(nums[i++] === target) {
        count++;
    }
    return count;
};
```

#### Thoughts

+ 1、这道题实在太简单了，有序数组，给出目标值，还能怎么做？找到一左一右的位置下标相减加1即可，不过如果找不到该目标值的位置，就返回0，判断一下就好。

+ 2、更简单的，filter过滤一下然后返回其长度即可。

+ 3、不用接口的做法，就是自己老老实实写查找了，两种做法：1、双指针，一左一右，找到目标值然后下标相减加1，相遇了还没找到即返回0。2、二分法，找到目标值出现的第一个位置，然后从该位置向后找，直到找到与目标值不相等的元素，返回计数即可。