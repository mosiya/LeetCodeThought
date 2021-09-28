### 剑指 Offer 09. 用两个栈实现队列

#### 描述

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 1:
```md
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]

输出：[null,null,3,-1]
```
+ 示例 2:
```md
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]

输出：[null,-1,null,null,5,2]
```


#### 提示
```md
1. 1 <= values <= 10000

2. 最多会对 appendTail、deleteHead 进行 10000 次调用
```

### 解答

+ 解答 1
```js
var CQueue = function() {
    this.queue = [];
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.queue.push(value);
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(this.queue.length < 1) return -1;
    return this.queue.shift()
};

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```

+ 解答 2
```js
var CQueue = function() {
    this.push_stack = [];
    this.pop_stack = [];
};

/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.push_stack.push(value);
};

/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(this.push_stack.length < 1 && this.pop_stack.length < 1) return -1;

    if(this.pop_stack.length > 0) return this.pop_stack.pop();

    while(this.push_stack.length) {
        this.pop_stack.push(this.push_stack.pop());
    }
    return this.pop_stack.pop();
};

/**
 * Your CQueue object will be instantiated and called as such:
 * var obj = new CQueue()
 * obj.appendTail(value)
 * var param_2 = obj.deleteHead()
 */
```


#### Thoughts

+ 1、我大JS根本不需要什么两个栈，一个数组解决所有问题！

+ 2、正经解这道题，用两个栈来实现队列，一个用来入队，另一个用来出队。主要是在出队时需要注意，当出队的栈为空时，再将入队的栈倒到出队栈里，这样就保证了先进先出的顺序，很简单。