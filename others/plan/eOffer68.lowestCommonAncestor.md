### 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先

#### 描述

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

注意：本题与主站 235 题相同：https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8

输出: 6 

解释: 节点 2 和节点 8 的最近公共祖先是 6。
```
+ 示例 2:
```md
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4

输出: 2

解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```


#### 提示
```md
1. 所有节点的值都是唯一的。

2. p、q 为不同节点且均存在于给定的二叉搜索树中。
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
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
    if(root.val > q.val && root.val > p.val) return lowestCommonAncestor(root.left, p, q);
    if(root.val < p.val && root.val < q.val) return lowestCommonAncestor(root.right, p, q);
    return root;
};
```

#### Thoughts

+ 1、详细的题解在 235 了，这里只给出最简单的递归做法。尤其题目说明了是二叉搜索树，p和q的节点都存在，且所有节点的值都是唯一的，所以非常简单，都不需要判空，只要俩节点在同侧，则继续同侧往下递归，不同侧则直接返回当前的根节点即可。