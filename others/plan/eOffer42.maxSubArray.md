### 剑指 Offer 42. 连续子数组的最大和

#### 描述

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

注意：本题与主站 53 题相同：https://leetcode-cn.com/problems/maximum-subarray/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]

输出: 6

解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```


#### 提示
```md
1. 1 <= arr.length <= 10^5

2. -100 <= arr[i] <= 100
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let max = Math.max(), pre = 0;
    for(let num of nums) {
        pre = Math.max(pre + num, num);
        max = Math.max(max, pre);
    }
    return max;
};
```

#### Thoughts

+ 1、这也是动态规划的经典题，在53有详细的题解(但其实写得并不好)。在这里，遍历数组，决定当前元素单独成为一段的开始还是加入之前的区间，取决于当前元素与当前元素加上之前区间和的大小，然后不断更新最大值即可。