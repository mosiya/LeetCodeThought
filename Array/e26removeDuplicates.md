### 26. 删除排序数组中的重复项

#### 描述

给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。


来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
```
+ 示例 2:
```md
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
```


#### 说明

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```js
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let index = 1;
    let item = nums[0];
    let first = false;
    for(let i = 1; i < nums.length; i ++) {
        if(nums[i] == item) {
            if(!first) {
                index = i;
                first = true;
            }
        } else {
            nums[index] = nums[i];
            item = nums[i];
            index++
        }
    }
    return index
};
```

+ 解答 2
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    if(nums.length < 1) return nums.length;
    let slow = 0;
    for(let fast = 1; fast < nums.length; fast ++) {
        if(nums[slow] != nums[fast]) {
            nums[++slow] = nums[fast]
        }
    }
    return slow + 1
};
```

+ 解答 3
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    if(nums.length < 1) return nums.length;
    let slow = 0;
    for(let fast = 1; fast < nums.length; fast ++) {
        if(nums[slow] != nums[fast]) {
            slow++;
            if(slow != fast) {
                nums[slow] = nums[fast];
            }
        }
    }
    return slow + 1
};
```

#### Thoughts

+ 1、看到去重我就兴奋，结果发现不是我想的那种去重，而是要原地去重，最后返回去重后数组的长度。由于原数组是经过排序的，说明重复的元素必定相邻。
  
  故我最开始的想法就是先遍历整个数组，然后用一个变量index去储存需要被覆盖的第一个位置，此后就从这个位置开始放置后面不重复的元素

  而且这个变量只在第一次遇到重复元素的时候开始启用，之后只跟着不重复的元素进行更新，故设置了一个标记位first(后来证明都是无用功。。)
  
  再用一个变量item存储遍历过程中每一个不重复的第一个元素，当遍历的元素与之不相等时更新该变量

  最后返回记录位置的这个变量index即可

+ 2、看过答案后发现自己写的相等的那段判断其实是多余的。因为第一次重复的情况，index都是必定等于i的，这里的index在不重复的情况下其实一直跟着i在自增。

  在把我设置的first和item去除以后，可以得到一个解决很多数组问题的版本：快慢指针。

  使用一个快指针去遍历整个数组，使用一个慢指针记录放置不重复元素的下标。

  每当遇到快指针和慢指针的元素不重复时，就把快指针指向的元素放置在慢指针的下一位。直到遍历结束。

  最后返回慢指针加1。加1是由于慢指针是从0开始的，长度等于下标加1。

+ 3、上述做法还可以进行优化。考虑一个舞重复的排序数组，实际上不需要进行任何放置的操作。

  故优化的做法就是在快慢指针的元素不重复时，若两个指针的位置相等，则不进行赋值操作。



