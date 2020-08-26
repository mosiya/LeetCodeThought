### 面试题 16.15. 珠玑妙算

#### 描述

珠玑妙算游戏（the game of master mind）的玩法如下。

计算机有4个槽，每个槽放一个球，颜色可能是红色（R）、黄色（Y）、绿色（G）或蓝色（B）。例如，计算机可能有RGGB 4种（槽1为红色，槽2、3为绿色，槽4为蓝色）。作为用户，你试图猜出颜色组合。打个比方，你可能会猜YRGB。要是猜对某个槽的颜色，则算一次“猜中”；要是只猜对颜色但槽位猜错了，则算一次“伪猜中”。注意，“猜中”不能算入“伪猜中”。

给定一种颜色组合solution和一个猜测guess，编写一个方法，返回猜中和伪猜中的次数answer，其中answer[0]为猜中的次数，answer[1]为伪猜中的次数。

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems/master-mind-lcci

著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

#### 示例

+ 示例 :
```md
输入： solution="RGBY",guess="GGRR"

输出： [1,1]

解释： 猜中1次，伪猜中1次。
```


#### 提示
```md
1. len(solution) = len(guess) = 4

2. solution和guess仅包含"R","G","B","Y"这4种字符
```

### 解答

+ 解答 1
```js
/**
 * @param {string} solution
 * @param {string} guess
 * @return {number[]}
 */
var masterMind = function(solution, guess) {
    let answer = [0, 0], obj = {R: 0, G: 0, B: 0, Y: 0};
    solution = solution.split('');
    guess = guess.split('');
    for(let i = 0; i < 4; i++) {
        if(solution[i] === guess[i]) {
            answer[0]++;
            solution[i] = '';
            guess[i] = '';
        }
    }
    for(let i = 0; i < 4; i++) {
        if(obj[solution[i]] !== void 0) {
            obj[solution[i]]++;
        }
    }
    answer[1] = guess.filter(item => {
        if(obj[item]) {
            obj[item]--;
            return true;
        }
    }).length;
    return answer;
};
```

+ 解答 2
```js
/**
 * @param {string} solution
 * @param {string} guess
 * @return {number[]}
 */
var masterMind = function(solution, guess) {
    let map = new Map(), ans1 = 0, ans2 = 0;
    for(let i = 0; i < 4; i++) {
        let item = solution[i];
        map.set(item, map.has(item) ? map.get(item) + 1 : 1);
    }

    for(let i = 0; i < 4; i++) {
        if(solution[i] === guess[i]) {
            ans1++;
        }
        if(map.get(guess[i])) {
            ans2++;
            map.set(guess[i], map.get(guess[i]) - 1);
        }
    }
    return [ans1, ans2 - ans1];
};
// 或者
/**
 * @param {string} solution
 * @param {string} guess
 * @return {number[]}
 */
var masterMind = function(solution, guess) {
    let obj = {R: 0, G: 0, B: 0, Y: 0}, ans1 = 0, ans2 = 0;
    for(let i = 0; i < 4; i++) {
        obj[solution[i]]++;
    }

    for(let i = 0; i < 4; i++) {
        if(solution[i] === guess[i]) {
            ans1++;
        }
        if(obj[guess[i]]) {
            ans2++;
            obj[guess[i]]--;
        }
    }
    return [ans1, ans2 - ans1];
};
```

+ 解答 3
```js
/**
 * @param {string} solution
 * @param {string} guess
 * @return {number[]}
 */
var masterMind = function(solution, guess) {
    let arr = guess.split(''), count = 0, sum = 0;

    for(let i = 0; i < 4; i++) {
        if(solution[i] === guess[i]) {
            count++;
        }
        let index = arr.indexOf(solution[i]);
        if(index > -1) {
            ans2++;
            arr[index] = '';
        }
    }
    return [ans1, ans2 - ans1];
};
```

#### Thoughts

+ 1、这道题因为数据过于简单特殊了，反而处理得略显臃肿。我老想着用数组的方法，然后再把解法往上面靠，就写出了方法一，结果其实不是太满意。先统计了猜中的次数，然后把猜中的元素替换为空，然后再对剩下的元素存哈希表，再过滤出来伪猜中的元素求个数，最后得到了答案。

+ 2、看了解答，发现大家都是先求了猜中的，然后统计所有猜中和伪猜中的，再用总的减去猜中的来得到伪猜中的个数，因为总数比较好统计。于是用这种方法做了一遍，分别用map和object作为哈希表的方式，看起来map好像会快一些。

+ 3、看到了一个用一次遍历搞定的，主要是把guess存了数组，然后用的indexOf判断得到的总数，因为长度只有4比较简单，所以耗时也差不多。