### 剑指 Offer 06. 从尾到头打印链表

#### 描述

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：head = [1,3,2]

输出：[2,3,1]
```


#### 提示
```md
1. 0 <= 链表长度 <= 10000
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
 * @return {number[]}
 */
var reversePrint = function(head) {
    let array = [];
    while(head) {
        array.unshift(head.val);
        head = head.next;
    }
    return array;
};
```


#### Thoughts

+ 1、这道题简单到我不需要说了，也不想用多种方法来做了。链表真的很讨厌，我大JavaScript直接用数组unshift解决一切。完事