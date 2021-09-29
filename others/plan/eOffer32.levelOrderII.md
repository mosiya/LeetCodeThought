### 剑指 Offer 32 - II. 从上到下打印二叉树 II

#### 描述

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

注意：本题与主站 102 题相同：https://leetcode-cn.com/problems/binary-tree-level-order-traversal/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/

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
  [9,20],
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
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
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
            layer.push(node.val);
            node.left && stack.push(node.left);
            node.right && stack.push(node.right);
        }
        res.push(layer);
    }
    return res;
};
```

#### Thoughts

+ 1、具体的题解都在 102 题啦。做法其实跟 I 没有什么本质区别，就是多了一层数组而已，每次都把当前层的节点存到数组里然后推到结果数组里就好。

  不过奇怪的就是 I 和 102 都是中等题，到了 II 反而是简单题了，不知道怎么分类的，也不保持一致。