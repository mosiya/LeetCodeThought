### 剑指 Offer 25. 合并两个排序的链表

#### 描述

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：1->2->4, 1->3->4

输出：1->1->2->3->4->4
```


#### 限制
```md
0 <= 链表长度 <= 1000
```

### 解答

+ 解答 
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    if(!l1) return l2;
    if(!l2) return l1;
    if(l1.val <= l2.val) {
        l1.next = mergeTwoLists(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoLists(l1, l2.next);
        return l2;
    }
};
```


#### Thoughts

+ 只写了递归的方式，详见->21. 合并两个有序链表