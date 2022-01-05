### 剑指 Offer 39. 数组中出现次数超过一半的数字

#### 描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

注意：本题与主站 169 题相同：https://leetcode-cn.com/problems/majority-element/


来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]

输出: 2
```

#### 提示
```md
1 <= 数组长度 <= 50000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let count = 0, major;
    for(let num of nums) {
        if(num != major) {
            if(count == 0) {
                major = num;
                count = 1;
            } else {
                count--;
            }
        } else {
            count++;
        }
    }
    return major;
};
```


#### Thoughts

+ 1、既然一定存在多数元素，那么说明可以使用摩尔投票法来处理。具体做法就是保存一个多数元素，保存一个计数，若与该元素相等便计数加1，不同便相减。减为0则重新记录，直到最后留下来的那个元素，必定为多数元素。原理很简单，多数元素一定能抵抗住其他元素的抵消从而保留下来。