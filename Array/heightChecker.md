### Height Checker

#### description

Students are asked to stand in non-decreasing order of heights for an annual photo.

Return the minimum number of students that must move in order for all students to be standing in non-decreasing order of height.

Notice that when a group of students is selected they can reorder in any possible way between themselves and the non selected students remain on their seats.

#### Example

+ Example 1:
```md
Input: heights = [1,1,4,2,1,3]

Output: 3

Explanation: 

Current array : [1,1,4,2,1,3]

Target array  : [1,1,1,2,3,4]

On index 2 (0-based) we have 4 vs 1 so we have to move this student.

On index 4 (0-based) we have 1 vs 3 so we have to move this student.

On index 5 (0-based) we have 3 vs 4 so we have to move this student.
```
+ Example 2:
```md
Input: heights = [5,1,2,3,4]

Output: 5
```
+ Example 3:
```md
Input: heights = [1,2,3,4,5]

Output: 0
```

#### Constraints:
```md
1 <= heights.length <= 100

1 <= heights[i] <= 100
```

### Solution

+ solution 1
```js
/**
 * @param {number[]} heights
 * @return {number}
 */
var heightChecker = function(heights) {
    let sorted = heights.slice();
    sorted.sort((a, b) => a-b);
    let length = heights.filter((item, index) => item != sorted[index]).length;
    return length;
};
```

+ solution 2
```js
/**
 * @param {number[]} heights
 * @return {number}
 */
var heightChecker = function(heights) {
    let buckets = new Array(101).fill(0);
    for(let height of heights) {
        buckets[height]++
    }
    let j = 0;
    let count = 0;
    for(let i = 1; i < buckets.length; i ++) {
        while(buckets[i] > 0) {
            if(heights[j] !== i) {
                count++;
            }
            buckets[i]--;
            j++
        }
    }
    return count;
};
```

#### Thoughts

+ 1、首先想到的就是先排序，然后一一对比相应位置上的元素是否一致，不一致则计数加1，最终返回计数个数

+ 2、看了解答，发现除了一一对比元素的方式以外，还有一种优化的方法。

  可以看到，备注里提示了heights的元素和长度均不超过100。
  
  以前学习排序的时候就学过一种方法叫桶排序，专门针对元素的数值在一定范围的情况，比如满分为100分的十万考生的排序，如果用传统的排序方法，最好的快排的复杂度也是O(nlogn)。
  
  但是如果我们以分数为下标进行排序，只要将相同分数的考生放到同样下标的一个储存空间里去，那么只要一趟遍历就可以确定顺序了，毕竟同分数的考试排序可以看作是一样的。

  这里也是如此。以元素为下标进行数组储存，将得到的桶与原数组进行比较即可。优化了排序这部分的复杂度，使其从O(nlogn)降到到了O(n)。

  这里要注意的点，一是桶的初始化，要按可能的最长长度来创建，元素初始化为0，否则会导致类型问题的错误。二是桶下标元素的递减要与原数组下标的递增一一对应。