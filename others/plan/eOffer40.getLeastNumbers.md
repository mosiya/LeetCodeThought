### 剑指 Offer 40. 最小的k个数

#### 描述

输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：arr = [3,2,1], k = 2

输出：[1,2] 或者 [2,1]
```
+ 示例 2:
```md
输入：arr = [0,1,2,1], k = 1

输出：[0]
```


#### 提示
```md
1. 0 <= k <= arr.length <= 10000

2. 0 <= arr[i] <= 10000
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var getLeastNumbers = function(arr, k) {
    return arr.sort((a, b) => a - b).slice(0, k);
};
```

+ 解答 2
```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
var getLeastNumbers = function(arr, k) {
    if(k >= arr.length) return arr;
    function quickSort(l, r) {
        let [i, j] = [l, r];
        while(i < j) {
            while(i < j && arr[j] >= arr[l]) j--; 
            while(i < j && arr[i] <= arr[l]) i++;
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        [arr[i], arr[l]] = [arr[l], arr[i]];
        if(k < i) return quickSort(l, i - 1);
        if(k > i) return quickSort(i + 1, r);
        return arr.slice(0, k);
    }
    return quickSort(0, arr.length - 1);
};
```


#### Thoughts

+ 1、大概有三种做法，这里只列两种，一种最简单的就是直接排序然后取最小的k个元素即可。

+ 2、第二种是快排的变种。快排每次都使用一个基准，然后从左找到第一个大于等于基准的值，从右边找到第一个小于基准的值，然后两者进行交换，反复这个过程，直到所有左边的值都小于等于基准，所有右边的值都大于等于基准，再把这个基准放到停下来的位置上；接着对左右两边递归执行这个过程即可。

  而这里如何利用快排的思想来解题，关键在于比较停下来的位置i和k的大小。停下来的位置i左边元素都比右边的元素小，如果i刚好等于k，那么左边的元素不需要再排序就可以直接返回了；若不相等，如果i小于k，那么说明i的位置左边的元素不够多，那么我们对i右边进行递归，反之，对i左边进行递归，直到i等于k为止。

ps：之所以没写第三种做法，是因为需要利用到一个特殊的数据结构——大顶堆。其他语言有现成的可以用，js需要自己构造，因为有点麻烦所以这里就不写了。总的来说思路就是先放k个数到大顶堆里去，接着剩下的元素通过和堆顶元素比较，比堆顶元素小的就把堆顶元素去掉把新元素加进去，一直加到最后。这样，留在大顶堆里的k个数就是最小的k个数了。