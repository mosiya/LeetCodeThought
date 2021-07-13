### 面试题 02.06. 回文链表

#### 描述

编写一个函数，检查输入的链表是否是回文的。

进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？


来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/palindrome-linked-list-lcci/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入： 1->2

输出： false 
```
+ 示例 2:
```md
输入： 1->2->2->1

输出： true 
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
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(head) {
    let arr = [];
    while(head) {
        arr.push(head.val);
        head = head.next;
    }
    for(let i = 0; i < (arr.length >> 1); i++) {
        if(arr[i] != arr[arr.length - 1 - i]) {
            return false;
        }
    }
    return true;
};
```


#### Thoughts

+ 只写了最简单的做法，详见->234. 回文链表