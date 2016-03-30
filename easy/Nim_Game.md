# Nim Game

---

### 题目介绍：

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.





### 分析题目：

以前玩大航海时代的时候 有一个酒馆里边 就有这种类似的游戏。当时大概知道怎么能赢:只要剩下4枚（4的倍数）金币让对方选，就能赢。 因为每个人必须要选，所以 `1 + 3 = 4`；如果每个人只能选  `1~4` 枚的话，就应该是 `1 + 4 = 5` , 以下是自己的解题答案：

```js
/**
 * @param {number} n
 * @return {boolean}
 */
var canWinNim = function(n) {
    var num = n % 4;
    if (num === 0) {
        return false;
    }
    return true;
    
};
```





** LeetCode 地址: ** [https://leetcode.com/problems/nim-game/](https://leetcode.com/problems/nim-game/)
