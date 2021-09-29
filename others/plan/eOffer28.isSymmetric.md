### 剑指 Offer 28. 对称的二叉树

#### 描述

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3

注意：本题与主站 101 题相同：https://leetcode-cn.com/problems/symmetric-tree/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：root = [1,2,2,3,4,4,3]

输出：true
```
+ 示例 2:
```md
输入：root = [1,2,2,null,3,null,3]

输出：false
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
var isSymmetric = function(root) {
    function _isSymmetric(left, right) {
        if(left == null && right == null) {
            return true;
        }
        if(left == null ^ right == null || left.val != right.val) {
            return false;
        }
        return _isSymmetric(left.left, right.right) && _isSymmetric(left.right, right.left);
    }
    return _isSymmetric(root, root);
};
```


#### Thoughts

+ 1、这题的详解在 101 ，这里值给出递归的代码，判断左右子树是否对称，每次只判断当前层的节点，只要不为false，就可以继续递归判断下一层的子节点。