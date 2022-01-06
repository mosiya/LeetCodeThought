### 剑指 Offer 54. 二叉搜索树的第k大节点

#### 描述

给定一棵二叉搜索树，请找出其中第 k 大的节点的值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2

输出: 4
```
+ 示例 2:
```md
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1

输出: 4
```


#### 提示
```md
1 ≤ k ≤ 二叉搜索树元素个数
```

### 解答

+ 解答 1
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} k
 * @return {number}
 */
var kthLargest = function(root, k) {
    const stack = [root], res = [];
    while(stack.length) {
        const node = stack.shift();
        if(!node.left && !node.right) {
            res.push(node);
        } else {
            node.right && stack.unshift(node.right);
            stack.unshift(node);
            node.left && stack.unshift(node.left);
            node.left = null;
            node.right = null;
        }
    }
    return res[res.length - k].val;
};
```

+ 解答 2
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} k
 * @return {number}
 */
var kthLargest = function(root, k) {
    let res;
    function dfs(root) {
        if(!root) return;
        dfs(root.right);
        if(k === 0) return;
        if(--k === 0) res = root.val;
        dfs(root.left);
    }
    dfs(root);
    return res;
};
```


#### Thoughts

+ 1、最简单的做法，就是使用迭代将树的节点按从大到小的顺序存到数组中，接着取数组倒数第k个数的值即可。

+ 2、二叉搜索树从大到小的话，需利用倒序的中序遍历，也就是右-根-左的顺序进行递归遍历。每次递归都需要进行计数，到达k的时候记录当前值，就是要找的第k大的值。