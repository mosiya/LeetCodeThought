### 面试题 17.12. BiNode

#### 描述

二叉树数据结构TreeNode可用来表示单向链表（其中left置空，right为下一个链表节点）。实现一个方法，把二叉搜索树转换为单向链表，要求依然符合二叉搜索树的性质，转换操作应是原址的，也就是在原始的二叉搜索树上直接修改。

返回转换后的单向链表的头节点。

注意：本题相对原题稍作改动

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/binode-lcci

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 :
```md
输入： [4,2,5,1,3,null,6,0]

输出： [0,null,1,null,2,null,3,null,4,null,5,null,6]
```


#### 提示
```md
节点数量不会超过 100000。
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
 * @return {TreeNode}
 */
var convertBiNode = function(root) {
    if(!root) return root;
    let res = [];
    function inorder(root) {
        if(!root) return;
        inorder(root.left);
        res.push(root.val);
        inorder(root.right);
    }
    inorder(root);
    let node = root;
    for(let i = 0; i < res.length - 1; i++) {
        node.val = res[i];
        node.left = null;
        if(!node.right) node.right = new TreeNode();
        node = node.right;
    }
    node.val = res.pop();
    return root;
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
 * @return {TreeNode}
 */
var convertBiNode = function(root) {
    let prev = new TreeNode(0);
    const head = prev;
    function inorder(root) {
        if(!root) return;
        // 处理完所有左节点
        inorder(root.left);
        // root的左节点已经被处理完毕，所以可以设置为null
        root.left = null;
        // prev的右节点指向root
        prev.right = root;
        // prev指针移到root上
        prev = root;
        // 处理右节点
        inorder(root.right);
    }
    inorder(root);
    return head.right;
};
```

+ 解答 3
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
 * @return {TreeNode}
 */
var convertBiNode = function(root) {
    let prev = new TreeNode(0);
    const head = prev, stack = [];
    while(root || stack.length) {
        while(root) {
            stack.push(root);
            root = root.left;
        }
        root = stack.pop();
        root.left = null;
        prev.right = root;
        prev = root;
        root = root.right;
    }
    return head.right;
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
 * @return {TreeNode}
 */
var convertBiNode = function(root) {
    let prev = new TreeNode(0);
    const head = prev, stack = [root];
    while(stack.length) {
        const node = stack.shift();
        if(!node) continue;

        const {left, right} = node;
        if(!left && !right) {
            prev.right = node;
            prev = node;
        } else {
            node.right = null;
            node.left = null;
            stack.unshift(right);
            stack.unshift(node);
            stack.unshift(left);
        }
    }
    return head.right;
};
```

#### Thoughts

+ 1、这道题是链表简单难度的最后一题，实在是，我觉得也不简单。。。要是硬写，我也可以用第一种方法这么写，用例也不会测试我是否在原来的节点上执行的操作。所以我就直接一个中序遍历，取到了所有的值，然后遍历这些值，从根节点出发，逐个赋值，并把左节点赋值为null，右节点存在就不管，不存在就new一个新的，并且只遍历到倒数第二个值。最后一个值直接赋值，最后返回root

+ 2、绷不住了看了题解，用的是中序遍历的递归做法，主要是要用一个伪头结点去归一化所有的情况。注释做了一些解释，主要看理解吧

+ 3、既然可以用中序遍历的递归做法，也一定可以使用中序遍历的非递归做法。于是按照中序遍历的非递归做法改造了一下，把收集节点值的代码改成了伪头结点的赋值的代码，其他保持不变即可。

  我自己可理解的非递归做法为第二种，这里主要是要把node的左右节点都去掉，这样在处理该节点的时候就会和叶子节点有统一的判断和处理。

这道题也有点魔鬼！磨了我一天，终于改对了，最后一种写法，改得我怀疑人生。链表是魔鬼！跟树结合的链表更是！