### 面试题 16.17. 连续数列

#### 描述

给定一个整数数组，找出总和最大的连续数列，并返回总和。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/contiguous-sequence-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入： [-2,1,-3,4,-1,2,1,-5,4]

输出： 6

解释： 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

#### 进阶
```md
如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let sum = nums[0], maxSum = nums[0], len = nums.length;
    for(let i = 1; i < len; i++) {
        sum = sum < 0 ? nums[i] : sum + nums[i];
        if(sum > maxSum) {
            maxSum = sum;
        }
    }
    return maxSum;
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let len = nums.length;
    for(let i = 1; i < len; i++) {
        nums[i] = nums[i - 1] < 0 ? nums[i] : nums[i] + nums[i - 1];
    }
    return Math.max(...nums);
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    return maxSum(0, nums.length - 1, nums);
};
function maxSum(left, right, nums) {
    if(left === right) return nums[left];
    let mid = (left + right) >> 1;
    let leftMaxSum = maxSum(left, mid, nums);
    let rightMaxSum = maxSum(mid + 1, right, nums);

    let leftBorderSum = -Infinity;
    let rightBorderSum = -Infinity;

    let sum = 0;

    for(let i = mid; i >= left; i--) {
        sum += nums[i];
        if(sum > leftBorderSum) leftBorderSum = sum;
    }

    sum = 0;

    for(let i = mid + 1; i <= right; i++) {
        sum += nums[i];
        if(sum > rightBorderSum) rightBorderSum = sum;
    }

    return Math.max(leftMaxSum, rightMaxSum, leftBorderSum + rightBorderSum);
}
```

#### Thoughts

+ 1、这道题之前已经做过了，刚拿到的时候有种做烂了的感觉。总之，用自认为最简单的方案做完了。第一种方案的关键就是用两个变量记录当前最大和以及整体最大和。

+ 2、这种方案主要就是数组去存下每次累加的最大值，最后求其中的最大值。关键就是，前一个求和小于0就丢弃。

+ 3、题目要求了分治的做法，我一直学不会，找解答一个比较靠谱的，默写了一遍。精妙的分治做法，不确定精妙在哪，只觉得每次看代码都很晕，因为有递归。实际上这种做法理解以后就不难，不理解的时候，不要通过看代码的方式实现，真的很费劲。

+ ps：此题与 e53 题一模一样！