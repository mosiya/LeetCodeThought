### 面试题 02.01. 移除重复节点

#### 描述

编写代码，移除未排序链表中的重复节点。保留最开始出现的节点。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/remove-duplicate-node-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：[1, 2, 3, 3, 2, 1]

输出：[1, 2, 3]
```
+ 示例 2:
```md
输入：[1, 1, 1, 1, 2]

输出：[1, 2]
```


#### 提示
```md
1. 链表长度在[0, 20000]范围内。

2. 链表元素在[0, 20000]范围内。
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
 * @return {ListNode}
 */
var removeDuplicateNodes = function(head) {
    if(!head || !head.next) return head;
    let set = new Set(), node = head;
    while(node) {
        set.add(node.val);
        if(node.next && set.has(node.next.val)) {
            const next = node.next;
            node.next = next.next;
            next.next = null;
        } else {
            node = node.next
        }
    }
    return head;
};
```


#### Thoughts

+ 1、对于未排序的链表删除重复节点，除了使用哈希表，我想不到别的方案了，看了官解发现要么用哈希表要么用双重循环。而双重循环会超时，所以只能用哈希表了。

  所以代码很简单，存下每个节点的值，重复的就删除即可。