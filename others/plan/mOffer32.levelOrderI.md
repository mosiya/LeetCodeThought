### 剑指 Offer 32 - I. 从上到下打印二叉树

#### 描述

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回：

[3,9,20,15,7]
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
 * @return {number[]}
 */
var levelOrder = function(root) {
    if(!root) return [];
    const res = [], stack = [root];
    while(stack.length) {
        let len = stack.length;
        while(len--) {
            let node = stack.shift();
            res.push(node.val);
            node.left && stack.push(node.left);
            node.right && stack.push(node.right);
        }
    }
    return res;
};
```

#### Thoughts

+ 1、老生常谈的层序遍历题了。关键点在于每次遍历栈的时候都保存当前栈的长度，然后进行遍历出队和子节点入队。应该已经很熟练了，就不多说了。