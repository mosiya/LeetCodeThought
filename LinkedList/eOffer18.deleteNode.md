### 剑指 Offer 18. 删除链表的节点

#### 描述

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入: head = [4,5,1,9], val = 5

输出: [4,1,9]

解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```
+ 示例 2:
```md
输入: head = [4,5,1,9], val = 1

输出: [4,5,9]

解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```


#### 提示
```md
1. 题目保证链表中节点的值互不相同

2. 若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点
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
 * @param {number} val
 * @return {ListNode}
 */
var deleteNode = function(head, val) {
    if(!head) return null;
    if(head.val == val) {
        return deleteNode(head.next, val);
    } else {
        head.next = deleteNode(head.next, val);
        return head;
    }
};
```


#### Thoughts

+ 只写了递归的方式，详见->203. 移除链表元素