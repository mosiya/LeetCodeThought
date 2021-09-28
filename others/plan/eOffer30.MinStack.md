### 剑指 Offer 30. 包含min函数的栈

#### 描述

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 :
```md
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```


#### 提示
```md
各函数的调用总次数不超过 20000 次
```

### 解答

+ 解答 1
```js
/**
 * initialize your data structure here.
 */
var MinStack = function() {
    this.minStack = [];
    this.stack = [];
    this.length = 0;
};

/** 
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function(x) {
    this.stack.push(x);
    if(this.length < 1) {
        this.minStack.push(x);
    } else {
        let min = this.minStack[this.length - 1];
        this.minStack.push(Math.min(x, min));
    }
    this.length++;
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    if(this.length < 1) return;
    this.stack.pop();
    this.minStack.pop();
    this.length--;
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    if(this.length < 1) return -1;
    return this.stack[this.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.min = function() {
    if(this.length < 1) return -1;
    return this.minStack[this.length - 1];
};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */
```


#### Thoughts

+ 1、此题与 155 基本一致，具体题解参考 155 题。这里给出带辅助栈的最优解，即每次push的时候都只往辅助栈中push当前的最小值即可，其他操作就跟stack一致。