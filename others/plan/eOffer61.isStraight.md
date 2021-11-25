### 剑指 Offer 61. 扑克牌中的顺子

#### 描述

从若干副扑克牌中随机抽 5 张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: [1,2,3,4,5]

输出: True
```
+ 示例 2:
```md
输入: [0,0,1,2,5]

输出: True
```


#### 提示
```md
1. 数组长度为 5 

2. 数组的数取值为 [0, 13] .
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var isStraight = function(nums) {
    nums.sort((a, b) => a - b);
    const count = nums.filter(item => item == 0).length, index = nums.findIndex(item => item !== 0);
    let miss = 0;
    for(let i = index + 1; i < 5; i++) {
        if(nums[i] == nums[i - 1]) return false;
        miss += nums[i] - nums[i - 1] - 1;
    }
    return miss <= count;
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var isStraight = function(nums) {
    nums.sort((a, b) => a - b);
    const index = nums.findIndex(item => item !== 0);
    for(let i = index + 1; i < 5; i++) {
        if(nums[i] == nums[i - 1]) return false;
    }
    return nums[4] - nums[index] < 5;
};
// 或者
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var isStraight = function(nums) {
    nums.sort((a, b) => a - b);
    let joker = 0;
    for(let i = 0; i < 4; i++) {
        if(nums[i] == 0) {
            joker++;
            continue;
        }
        if(nums[i] == nums[i + 1]) return false;
    }
    return nums[4] - nums[joker] < 5;
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var isStraight = function(nums) {
    let set = new Set, min = Math.min(), max = Math.max();
    for(let i = 0; i < 5; i++) {
        if(nums[i] === 0) continue;
        if(set.has(nums[i])) return false;
        set.add(nums[i]);
        min = Math.min(min, nums[i]);
        max = Math.max(max, nums[i]);
    }
    return max - min < 5;
};
```

#### Thoughts

+ 1、经过了各种调试，我自己写出了第一版可以通过的代码。主要思路是，先排序、筛选出王的个数、确定王的位置，接着就从王的下一个位置开始遍历，若遇到重复的牌则直接返回false，否则统计两个牌的差值-1，最后看缺的部分是否能被王来填补即可。

+ 2、在方法1的基础上，我觉得可以不需要统计每两个不为王的牌的差值，既然已经排序，直接计算最大和最小的两个不为王的牌的差值，看是否小于5即可。其中除了王以外不可以出现重复的牌，故只要遍历判断是否需要提前返回false即可。

  根据官解也可以得到另一种类似的做法，可以不提前找到王的位置，在遍历的时候做这件事。但我觉得我的写法更好看些，哈哈。

+ 3、既然是判断除了王以外最大最小两个牌的差值是否小于5，那么还可以不排序进行这个操作。

  具体来说就在，在遍历的过程中去寻找最大牌和最小牌，最后计算差值即可；
  
  在这个遍历的过程中，我们如果找到相同的牌，要提前返回，故采用一个集合来记录出现过的牌，若之前已出现则直接返回false；

  但有一种情况是特殊的需要排除，就是大小王，于是提前判断，若牌是大小王，忽略即可。