### 剑指 Offer 32 - III. 从上到下打印二叉树 III

#### 描述

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

来源：力扣（LeetCode）



著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]
```


#### 提示
```md
节点总数 <= 1000
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
 * @return {number[][]}
 */
var levelOrder = function(root) {
    if(!root) return [];

    let stack = [root], res = [], flag = true;
    while(stack.length) {
        let len = stack.length, layer = [];
        while(len--) {
            if(flag) {
                const node = stack.shift();
                layer.push(node.val);
                node.left && stack.push(node.left);
                node.right && stack.push(node.right);
            } else {
                const node = stack.pop();
                layer.push(node.val);
                node.right && stack.unshift(node.right);
                node.left && stack.unshift(node.left);
            }
        }
        res.push(layer);
        flag = !flag;
    }
    return res;
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
 * @return {number[][]}
 */
var levelOrder = function(root) {
    if(!root) return [];

    const stack = [root], res = [];
    let flag = true;
    while(stack.length) {
        let len = stack.length;
        const layer = [];
        while(len--) {
            const node = stack.shift();
            flag ? layer.push(node.val) : layer.unshift(node.val);
            node.left && stack.push(node.left);
            node.right && stack.push(node.right);
        }
        res.push(layer);
        flag = !flag;
    }
    return res;
};
// 或者
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
    if(!root) return [];

    const stack = [root], res = [];
    while(stack.length) {
        let len = stack.length;
        const layer = [];
        while(len--) {
            const node = stack.shift();
            res.length & 1 ? layer.unshift(node.val) : layer.push(node.val);
            node.left && stack.push(node.left);
            node.right && stack.push(node.right);
        }
        res.push(layer);
    }
    return res;
};
```

#### Thoughts

+ 1、这道题是之字形按层打印，所以需要做一些判断和处理。第一层是正序，第二层是逆序，第三层是正序，以此类推。

  我是使用了一个变量来判断，正序的时候，执行出队，子节点入队的过程；逆序时，执行出栈，然后子节点逆着从头部插入的过程。

  由于每次取节点存子节点都是一个方向，所以不会出现阻塞的问题。

+ 2、除了在存取节点的时候做判断，其实还可以在遍历输出的时候做判断处理，比如正序的时候用的是尾部插入，逆序的时候是头部插入，这样就比1的处理更少了。

  而且对于正逆序的判断，还可以用结果数组长度的奇偶来判定。当前结果数组的长度为偶数的时候为正序，奇数的时候为逆序。比如结果数组为空时，长度为0是偶数，要存的第一行为正序输出；当存完第一行后，结果数组长度为1是奇数，要存的第二行为逆序输出。

  于是得到结果。