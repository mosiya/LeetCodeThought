### 面试题 02.02. 返回倒数第 k 个节点

#### 描述

实现一种算法，找出单向链表中倒数第 k 个节点。返回该节点的值。

注意：本题相对原题稍作改动


来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入： 1->2->3->4->5 和 k = 2

输出： 4
```


#### 说明
```md
给定的 k 保证是有效的。
```

### 解答

+ 解答 1
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {number}
 */
var kthToLast = function(head, k) {
    let node = head, node_k = head;
    while(k-- > 0) {
        node = node.next;
    }
    while(node) {
        node = node.next;
        node_k = node_k.next;
    }
    return node_k.val;
};
```

+ 解答 2
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {number}
 */
var kthToLast = function(head, k) {
    let node = head, node_k = head, t = 0;
    while(node) {
        node = node.next;
        if(t++ >= k) node_k = node_k.next;
    }
    return node_k.val;
};
```


#### Thoughts

+ 1、这道题还用说吗？跟剑指 Offer 22. 链表中倒数第k个节点几乎一模一样，除了最后需要返回节点的值以外，没啥区别。双指针，解决

+ 2、双指针加控制变量，过