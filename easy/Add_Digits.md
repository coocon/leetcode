# Add Digits 

---

### 题目介绍：

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

For example:

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up:
Could you do it without any loop/recursion in O(1) runtime?



### 分析题目：

如果可以用循环或者递归解题会比较简单，暂不考虑 js 的数据类型 `Number` 的极限值，解题如下：


```js
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {
    
    function addDigit (num) {
        var str = num + ''; 
        var res = 0
        for (var i = 0; i < str.length; i++) {
            res += parseInt(str[i], 0); 
        }
        if (res < 10) {
            return res;
        }
        else {
            return addDigit(res); 
        }
    }
    
    return addDigit(num);
};
```

以上解法又是循环又是递归的，不符合题目的要求，所以要换一个思路。多写几个例子：

* 如果 `num < 10` 直接返回，不用做运算。 
* 如果是 `10` 则要 `1 + 0 =  1` ， 相当于初始值 `1`。
* 如果是 `11` 则要 `1 + 1 =  2` ， 相当于初始值 `2`。
* 如果是 `12` 则要 `1 + 2 =  3` ， 相当于初始值 `3`。
* 如果是 `99` 则要 `9 + 9 = 18 = 1 + 8 = 9`。
* 如果是 `100` 则要 `1 + 0 + 0 =  1`。
* 如果是 `109` 则要 `1 + 0 + 9  =  10  >  1 + 0 = 1 `。


看上去 `12 - 3 = 9`, `11 - 2 = 9`, `100 - 1 = 99`, `109 - 1 = 108`: 假设结果是 `f(num)`, 初始值是 `num` , 这样看来 `num` - `f(num)` 是 `9` 的倍数: `n`。

先这么写：`f(num)` = `num - 9 * n`; n 是多少呢, `n = (num - f(num) ) / 9` ,因为f(num)是 `1~9` (num >= 10的情况下)


继续看如果
    * `f(num) == 9`: `n = Floor(num / 9) - 1`;
    *  `f(num) !=9` `n = Floor(num / 9)` ，

综合一下得：`n = Floor(num - 1 / 9)`。


代入上边的公式得：

`f(num)` = `num - Floor((num - 1) / 9) * 9` 。






想想还有点小激动呢。 根据这个公式的结果是: 


```js
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {

   var n = num - parseInt((num - 1) / 9, 10) * 9;
   return n; 
};
```

### 补充

今天早上查了点资料，发现结果跟mod(9)有关系，如下：

* 如果num === 0: f(num) = 0;
* 如果num !== 0: num % 9 === 0: f(num) = 9;
* 如果num !==0 并且 num % 9 !== 0: f(num) = num % 9;


```js
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {
    if (num === 0) {
        return 0;
    }
    var n = num % 9;
    if (n === 0) {
        n = 9;
    }
    return n;
};
```

随即又提交了一版。

上边的解法还是不够精简，最终整合成以下简单的写法：

```js
/**
 * @param {number} num
 * @return {number}
 */
var addDigits = function(num) {

    return 1 + (num - 1) % 9;
};
```


** LeetCode 地址: ** [https://leetcode.com/problems/add-digits/](https://leetcode.com/problems/add-digits/)
