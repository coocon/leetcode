# Minimum Depth of Binary Tree

---

### 题目介绍：

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.



### 分析题目：

二叉树获取到叶子节点的最短深度，叶子节点的 `left` 和 `right` 都是 `null`，如果节点的 `left` 为 `null` 并且 `right` 不是 `null`，需要继续递归调用函数（参数是 `root.right`)，反之亦然。 如果 `left` 和 `right` 同时存在，就选最小的那个。于是解题如下：


```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function(root) {
    if (root === null) {
        return 0;
    }
    var left = minDepth(root.left);
    var right = minDepth(root.right);
    if (left === 0 || right === 0) {
        return left + right + 1;
    }
    return (left > right ? right : left) + 1;
    
};
```


** LeetCode 地址: ** [https://leetcode.com/problems/minimum-depth-of-binary-tree/](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
