### 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面

#### 描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数在数组的前半部分，所有偶数在数组的后半部分。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：nums = [1,2,3,4]

输出：[1,3,2,4] 

注：[3,1,2,4] 也是正确的答案之一。
```


#### 提示
```md
1. 0 <= nums.length <= 50000

2. 0 <= nums[i] <= 10000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var exchange = function(nums) {
    let left = 0, right = nums.length - 1;
    while(left < right) {
        if(!(nums[left] & 1) && (nums[right] & 1)) {
            [nums[left], nums[right]] = [nums[right], nums[left]];
        } else if(nums[left] & 1) {
            left++;
        } else {
            right--;
        }
    }
    return nums;
};
```


#### Thoughts

+ 1、这道题很简单，双指针首尾扫描，左边遇到偶数，右边遇到奇数，就进行原地交换即可。这里判断为奇数的方法是 & 1 ，也可以判断 % 2，个人更喜欢 & 1 ，因为有种一眼看过去就知道是奇数的感觉，哈哈。