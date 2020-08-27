### 面试题 10.01. 合并排序的数组

#### 描述

给定两个排序后的数组 A 和 B，其中 A 的末端有足够的缓冲空间容纳 B。 编写一个方法，将 B 合并入 A 并排序。

初始化 A 和 B 的元素数量分别为 m 和 n。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/sorted-merge-lcci

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 :
```md
输入:
A = [1,2,3,0,0,0], m = 3

B = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```


#### 提示
```md
A.length == n + m
```

### 解答

+ 解答 1
```js
/**
 * @param {number[]} A
 * @param {number} m
 * @param {number[]} B
 * @param {number} n
 * @return {void} Do not return anything, modify A in-place instead.
 */
var merge = function(A, m, B, n) {
    let i = 0, j = 0, arr = A.slice(0, m);
    for(let k = 0; k < m + n; k++) {
        if(i === m || j === n) break;
        if(arr[i] <= B[j]) {
            A[k] = arr[i];
            i++;
        } else {
            A[k] = B[j];
            j++;
        }
    }
    if(i === m) {
        for(let k = m + j; k < m + n ; k++) {
            A[k] = B[j];
            j++;
        }
    } else {
        for(let k = n + i; k < m + n; k++) {
            A[k] = arr[i];
            i++;
        }
    }
};
// 或者
/**
 * @param {number[]} A
 * @param {number} m
 * @param {number[]} B
 * @param {number} n
 * @return {void} Do not return anything, modify A in-place instead.
 */
var merge = function(A, m, B, n) {
    let i = 0, j = 0, arr = A.slice(0, m), k = 0;
    while(i < m && j < n) {
        A[k++] = arr[i] <= B[j] ? arr[i++] : B[j++];
    }
    while(i < m) {
        A[k++] = arr[i++];
    }
    while(j < n) {
        A[k++] = B[j++];
    }
};
```

+ 解答 2
```js
/**
 * @param {number[]} A
 * @param {number} m
 * @param {number[]} B
 * @param {number} n
 * @return {void} Do not return anything, modify A in-place instead.
 */
var merge = function(A, m, B, n) {
    for(let i = m, j = 0; i < m + n; i++, j++) {
        A[i] = B[j];
    }
    A.sort((a, b) => a - b);
};
```

+ 解答 3
```js
/**
 * @param {number[]} A
 * @param {number} m
 * @param {number[]} B
 * @param {number} n
 * @return {void} Do not return anything, modify A in-place instead.
 */
var merge = function(A, m, B, n) {
    let i = m - 1, j = n - 1;
    for(let k = m + n - 1; k >= 0; k--) {
        if(i < 0 || j < 0) break;
        if(A[i] >= B[j]) {
            A[k] = A[i];
            i--;
        } else {
            A[k] = B[j];
            j--;
        }
    }
    if(i < 0) {
        for(let k = 0; k <= j; k++) {
            A[k] = B[k];
        }
    }
};
// 或者
/**
 * @param {number[]} A
 * @param {number} m
 * @param {number[]} B
 * @param {number} n
 * @return {void} Do not return anything, modify A in-place instead.
 */
var merge = function(A, m, B, n) {
    let i = m - 1, j = n - 1, k = m + n - 1;
    while(i >= 0 && j >= 0) {
        A[k--] = A[i] >= B[j] ? A[i--] : B[j--];
    }
    while(j >= 0) {
        A[k--] = B[j--];
    }
};
```

#### Thoughts

+ 1、其实做过类似的，一开始就想到了从后往前遍历放置元素，简单易操作。不过还是从别的方法开始做一遍再说。比如说方法一，先使用另一个数组来保存A的前m个元素，然后从头开始遍历，通过判断两个数组元素的大小来放置元素到A数组中去。最后会有一个数组先遍历完毕，然后再将未完的数组的元素逐次放到剩下的位置中去。

  这个过程中，麻烦的就是需要判断两个数组是否有遍历完成的，然后根据不同情况放置剩下的那个数组的元素。

  看了一下，这个方法可以写得很简单，比如第一个for循环可以改成while循环，这个k是不可能到达m+n-1处的，一定是i或者j先到达尽头，于是更改了while判断条件。然后剩下的也不需要分别判断，直接每种都再while一遍，有剩下元素未遍历的就会进入到对应的循环中，而下标加1的操作也可以直接写到赋值里去，一行就可以搞定。

+ 2、看了解答，有个最简单好理解的做法就是，把B数组的所有元素一股脑放到A中去，然后排序就完事。简单明了，就是时间复杂度是O(nlogn)的。

+ 3、这个方法是我一开始就想到了的，但是写的过程就跟方法一的第一种写法那样，写得不够简洁优雅，于是又改进了一下得到了第二种写法。

  这里的遍历会更简单一些，也不需要再额外存一个A数组的元素了，因为从后向前遍历，要么B数组先遍历完，剩下的A数组的元素就不需要再动了，要么就是A数组的元素先遍历完，此时只要再处理一下B数组剩下的元素即可。赋值的判断可以使用三元判断，减1的做法可以写到赋值里去，一行就可以搞定。

  注意处理B数组剩下的元素时，不可以用A[j--] = B[j--]，因为前一个j--会先减1，这样到了B这边就会再减1，就错了。A的赋值需要用k来遍历。