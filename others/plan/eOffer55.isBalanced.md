### 剑指 Offer 55 - II. 平衡二叉树

#### 描述

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

注意：本题与主站 110 题相同：https://leetcode-cn.com/problems/balanced-binary-tree/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。
```
+ 示例 2:
```md
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
```


#### 提示
```md
0 <= 树的结点个数 <= 10000
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
 * @return {boolean}
 */

function getHeight(node) {
    if(!node) return 0;
    return 1 + Math.max(getHeight(node.left), getHeight(node.right));
}

var isBalanced = function(root) {
    if(!root) return true;
    if(Math.abs(getHeight(root.left) - getHeight(root.right)) > 1) {
        return false;
    } else {
        return isBalanced(root.left) && isBalanced(root.right);
    }
};
```

#### Thoughts

+ 1、这道题的详细题解键 110 题，这里给出最好理解的做法，使用一个函数去获取树的高度，然后根据高度差是否超过1来判断返回false或true