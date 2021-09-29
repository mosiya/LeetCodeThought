### 剑指 Offer 27. 二叉树的镜像

#### 描述

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1

注意：本题与主站 226 题相同：https://leetcode-cn.com/problems/invert-binary-tree/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：root = [4,2,7,1,3,6,9]

输出：[4,7,2,9,6,3,1]
```


#### 提示
```md
0 <= 节点个数 <= 1000
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
var mirrorTree = function(root) {
    if(!root) return root;
    [root.left, root.right] = [mirrorTree(root.right), mirrorTree(root.left)];
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
var mirrorTree = function(root) {
    if(!root) return root;
    let stack = [root];
    while(stack.length) {
        const node = stack.shift();
        
        node.left && stack.push(node.left);
        node.right && stack.push(node.right);
        [node.left, node.right] = [node.right || null, node.left || null];
    }
    return root;
};
```


#### Thoughts

+ 1、本题在 226 有详解，这里给出最简单的递归代码。只要将左右节点赋值为翻转后的左右节点即可。

+ 2、在翻看了原来题目我的迭代解法后，我发现可以写得更简单，于是在这里再贴一下代码：使用栈来保存节点，取下节点并存入子节点，然后交换左右节点即可。