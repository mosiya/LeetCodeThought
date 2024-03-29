### 剑指 Offer 11. 旋转数组的最小数字

#### 描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

注意：本题与主站 154 题相同：https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：[3,4,5,1,2]

输出：1
```
+ 示例 2:
```md
输入：[2,2,2,0,1]

输出：0
```


### 解答

+ 解答 1
```js
/**
 * @param {number[]} numbers
 * @return {number}
 */
var minArray = function(numbers) {
    return Math.min(...numbers);
};
```

+ 解答 2
```js
/**
 * @param {number[]} numbers
 * @return {number}
 */
var minArray = function(numbers) {
    let left = 0, right = numbers.length - 1;
    if(numbers[left] < numbers[right]) return numbers[left];
    while(numbers[left] == numbers[right]) {
        right--;
    }
    while(left < right) {
        let mid = left + right >> 1;
        if(numbers[mid] > numbers[right]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return numbers[left];
};
```

+ 解答 3
```js
/**
 * @param {number[]} numbers
 * @return {number}
 */
var minArray = function(numbers) {
    let left = 0, right = numbers.length - 1;
    while(left < right) {
        let mid = left + right >> 1;
        if(numbers[mid] > numbers[right]) {
            left = mid + 1;
        } else if(numbers[mid] < numbers[right]) {
            right = mid;
        } else {
            right--;
        }
    }
    return numbers[left];
};
```

#### Thoughts

+ 1、简单题就要有简单题的样子，直接求最小值就对了【不是】

+ 2、正经来做，详细的题解可以看 154 题，这里就不细说了