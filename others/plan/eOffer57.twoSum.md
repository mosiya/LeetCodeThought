### 剑指 Offer 57. 和为s的两个数字

#### 描述

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：nums = [2,7,11,15], target = 9

输出：[2,7] 或者 [7,2]
```
+ 示例 2:
```md
输入：nums = [10,26,30,31,47,60], target = 40

输出：[10,30] 或者 [30,10]
```


#### 提示
```md
1. 1 <= nums.length <= 10^5

2. 1 <= nums[i] <= 10^6
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let left = 0, right = nums.length - 1;
    while(left < right) {
        const sum = nums[left] + nums[right];
        if(sum === target) {
            return [nums[left], nums[right]];
        } else if(sum > target) {
            right--;
        } else {
            left++;
        }
    }
    return [];
};
```


#### Thoughts

+ 1、数组都是有序的了，找和为指定值的，双指针首尾扫描即可，没有什么好说的，非常简单的题，过。