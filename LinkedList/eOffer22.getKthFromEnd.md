### 剑指 Offer 22. 链表中倒数第k个节点

#### 描述

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.
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
 * @return {ListNode}
 */
var getKthFromEnd = function(head, k) {
    let node = head, node_k = head;
    while(k-- > 0) {
        node = node.next;
    }
    while(node) {
        node = node.next;
        node_k = node_k.next;
    }
    return node_k;
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
 * @return {ListNode}
 */
var getKthFromEnd = function(head, k) {
    let node = head, node_k = head, t = 0;
    while(node) {
        node = node.next;
        if(t++ >= k) node_k = node_k.next;
    }
    return node_k;
};
```


#### Thoughts

+ 1、这道题也很简单，用两个节点，一个先走k步，然后两个节点再一起走。当先走的节点到达终点，那么后走的节点就到达了倒数第k个节点处

+ 2、可以加一个变量进行控制，当t >= k的时候，后面的节点再跟着一起走