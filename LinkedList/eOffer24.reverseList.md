### 剑指 Offer 24. 反转链表

#### 描述

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 :
```md
输入: 1->2->3->4->5->NULL

输出: 5->4->3->2->1->NULL
```


#### 限制
```md
0 <= 节点个数 <= 5000
```

### 解答

+ 解答 1
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    if(!head || !head.next) return head;

    const new_head = reverseList(head.next);
    head.next.next = head;
    head.next = null;
    return new_head;
};
```


#### Thoughts

+ 只写了递归的模式，详见->206. 反转链表