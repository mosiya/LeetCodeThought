### 剑指 Offer 35. 复杂链表的复制

#### 描述

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

注意：本题与主站 138 题相同：https://leetcode-cn.com/problems/copy-list-with-random-pointer/

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e1.png)
```md
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]

输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```
+ 示例 2:
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e2.png)
```md
输入：head = [[1,1],[2,1]]

输出：[[1,1],[2,1]]
```
+ 示例 3:
![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/01/09/e3.png)
```md
输入：head = [[3,null],[3,0],[3,null]]

输出：[[3,null],[3,0],[3,null]]
```
+ 示例 4:
```md
输入：head = []

输出：[]

解释：给定的链表为空（空指针），因此返回 null。
```


#### 提示
```md
1. -10000 <= Node.val <= 10000

2. Node.random 为空（null）或指向链表中的节点。

3. 节点数目不超过 1000 。
```

### 解答

+ 解答 1
```js
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function(head) {
    if(!head) return null;
    let map = new Map();
    for(let node = head; node !== null; node = node.next) {
        map.set(node, new Node(node.val));
    }
    for(let node = head; node !== null; node = node.next) {
        map.get(node).next = map.get(node.next) || null;
        map.get(node).random = map.get(node.random) || null;
    }
    return map.get(head);
};
```


#### Thoughts

+ 1、这道题与 138 题一样，所以在 138 题可找到详细的题解。这里给最优雅的实现方式，先将原节点与新节点创建一一对应的映射关系，然后再使用这个映射表建立next和random指针，最后返回head对应的节点即可。注意空节点的赋值默认为null。