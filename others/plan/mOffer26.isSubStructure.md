### 剑指 Offer 26. 树的子结构

#### 描述

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：A = [1,2,3], B = [3,1]

输出：false
```
+ 示例 2:
```md
输入：A = [3,4,5,1,2], B = [4,1]

输出：true
```


#### 提示
```md
0 <= 节点个数 <= 10000
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
 * @param {TreeNode} A
 * @param {TreeNode} B
 * @return {boolean}
 */
var isSubStructure = function(A, B) {
    if(!A || !B) return false;
    return check(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
};

function check(A, B) {
    const stack1 = [A], stack2 = [B];
    while(stack2.length) {
        const node1 = stack1.shift(), node2 = stack2.shift();
        if(!node2) continue;
        if(!node1 || node1.val !== node2.val) return false;

        stack1.push(node1.left, node1.right)
        stack2.push(node2.left, node2.right)
    }
    return true;
}
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
 * @param {TreeNode} A
 * @param {TreeNode} B
 * @return {boolean}
 */
var isSubStructure = function(A, B) {
    if(!A || !B) return false;
    return check(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
};

function check(A, B) {
    if(!B) return true;
    if(!A) return false;
    return A.val == B.val && check(A.left, B.left) && check(A.right, B.right);
}
```

#### Thoughts

+ 1、两种做法的主体部分是一样的，若A或者B为空都返回false。接着判断B是否为A的子结构，或者再对A的左右子树递归调用主函数。

不同的地方在于同构子树的判定，可以用递归，也可以用迭代。我当初在做这道题的时候，是用的迭代，但是那时候的代码是错误的，我贴在这里警醒自己：

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} A
 * @param {TreeNode} B
 * @return {boolean}
 */

var isSubStructure = function(A, B) {
    if(!A || !B) return false;
    if(A.val == B.val) {
        if(check(A, B)) return true;
    }
    return isSubStructure(A.left, B) || isSubStructure(A.right, B);
};

// 错误的做法！！
function check(A, B) {
    const stack1 = [A], stack2 = [B];
    while(stack2.length) {
        const node1 = stack1.shift(), node2 = stack2.shift();
        if(!node1 && !node2) continue;
        if(!node1 || !node2) return false;
        if(node1.val !== node2.val) return false;

        // 错误的地方！！
        node1.left && stack1.push(node1.left)
        node2.left && stack2.push(node2.left)
        node1.right && stack1.push(node1.right)
        node2.right && stack2.push(node2.right)
    }
    return true;
}
```

虽然是错误的做法，但是却通过了测试用例，说明这个测试用例是不全的。这里的错误在于，stack1和stack2都是只放入非空子节点，那么如果如果刚好A只有一个左子节点，B只有一个右子节点，它们刚好相等呢？这时候stack1和stack2取出来比较值的时候是觉察不出来的。

所以要么就不能判空，无论左右子节点是否为空都要放入栈中，这样可以保证放进去的子节点即使是空节点也是一一对应的。然后把关键的步骤放在取出节点以后的判断。

B栈取出的节点为空时continue，否则A栈取出的节点为空或者两个节点值不相等都返回false。当B栈为空都没有返回false，则返回true。

+ 2、check函数其实用递归的做法更简单。由于B是否为空已经在主函数里判断过了，所以这里一旦发现B为空，说明这个分支已经check通过了，所以返回true。而如果B不为空而A为空，那说明A比B少了节点，于是返回false。

  剩下的就是判断A和B的值是否相等以及左右子树是否分别相等。