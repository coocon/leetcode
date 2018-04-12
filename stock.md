# 求股票收益最大MAX

---

### 题目介绍：

有一支股票，已经把它的若干天内的价格记录成一个数组 prices
每天只可以买入 或者卖出一次， 假设从第一天开始计算，求收益最大


比如一个有一个数组：var prices = [10, 9, 26, 29, 1, 6, 5, 8, 12, 20, 10, 5, 10, 11];


### 分析题目：
每天只能交易一次， 买入或者卖出。 当然是必须先买入再可以卖出，不可以做空。
需要先解出来，只交易一次的话（即只买入一次，卖出一次），求收益最大 calMax
然后写出calMaxN，假定可以交易N的最大收益， 利用循环和递归，求解Math.max( calMaxN(i) = calMaxN(i - 1 ) +  calMaxN (1) )


```js
/**
 * @param {number} n
 * @return {boolean}
 */
var prices = [10, 9, 26, 29, 1, 6, 5, 8, 12, 20, 10, 5, 10, 11];
var changes = prices.map((item,index) => {
    return item - prices[index-1]
}).slice(1);

console.log('prices', prices);
console.log('changes:', changes);
//缓存计算结果
var cache = {};

function getCache(prices) {
    return cache[prices.join(',')];
}
function setCache(prices, value) {
    cache[prices.join(',')] = value;
}

function calMax(prices) {
    if (getCache(prices) !== undefined) {
        return getCache(prices);
    }

    var changes = prices.map((item,index) => {
        return item - prices[index-1]
    }).slice(1);
    var max = changes[0];
    var sum0 = changes[0];
    //初始买入
    var begin = 0;
    //初始卖出
    var end = begin + 1;
    for (var i = 1 ; i < changes.length; i++) {
        var sum1 = Math.max(sum0 + changes[i], changes[i]);
        if (sum1 > max) {
            max = sum1;
            if (sum0 + changes[i] > changes[i]) {
                end = i + 1;
            }
            else {
                begin = i + 1 - 1;
                end = begin + 1;
            }
        }
        sum0 = sum1;

        //console.log('sum0, sum1, max,', sum0, sum1, max)
        //console.log('begin, end,', prices[begin], prices[end])
    }
    //console.log('max: begin, end', max, ':', prices[begin], ',', prices[end])
    //设置缓存
    setCache(prices, max)
    return max;
}


/**
 * 计算买卖N次的最大值
 */
function calMaxN(prices, n) {
    var changes = prices.map((item,index) => {
        return item - prices[index-1]
    }).slice(1);
    var length = changes.length;
    if (n == 1) {
        return calMax(prices);
    }
    /* if (n == 2) {
     *     return calMax2(prices);
     * } */
    /* if (n == 3) {
     *     var max = calMaxN(prices, n - 1);
     *     var sum0 = max;
     *     for (var i = n-1; i < length - 1; i++) {
     *         sum0 = Math.max(calMaxN(prices.slice(0, i + 1), n-1) + calMaxN(prices.slice(i + 1), 1), max)
     *         if (sum0 >= max) {
     *             max = sum0;
     *         }
     *     }
     *     return Math.max(
     *         calMaxN(prices, n - 1),
     *         max
     *     )
     * } */
    var max = calMaxN(prices, n - 1);
    var sum0 = max;
    for (var i = n - 1; i < length - 1; i++) {
        sum0 = Math.max(calMaxN(prices.slice(0, i + 1), n-1) + calMaxN(prices.slice(i + 1), 1), max)
        if (sum0 > max) {
            max = sum0;
        }
    }
    return Math.max(
        calMaxN(prices, n - 1),
        max
    )
}


/**
 * 计算收益最大的函数
 */
function calMaxMain(prices) {
    var maxCalCount = Math.floor(prices.length / 2);
    var max = calMaxN(prices, maxCalCount);
    console.log('maxCalCount, max', maxCalCount, ',', max);
    return max;
}
console.log('max1, max2', calMaxN(prices, 1), calMaxN(prices, 2))
console.log('max3', calMaxN(prices, 3))
console.log('max4', calMaxN(prices, 4))
d = new Date().getTime();
calMaxMain(prices);
console.log(new Date().getTime() - d)
