# Maximum Depth of Binary Tree

---

### 题目介绍：

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.



### 分析题目：

二叉树获取最深节点的长度，第一想到的就是递归，因为树有 `left` 和 `right`，所以需要用 `Math.max` 函数获取两个分叉上的最大深度。默认节点长度是0，如果 `node` 本身不是 `null` 就递归调用函数计算对应的 `left` 和 `right` 的最大值，当然需要返回自身的 `len` : `1`。


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
var maxDepth = function(root) {
     
    var len = 0;
    if (!root) {
        return len;
    }
    len = 1;
    return len + Math.max(maxDepth(root.left), maxDepth(root.right));
    
};
```

问题是解决了，看网上的解题方法更清晰一些，但是思路是一样的，整理如下：

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
var maxDepth = function(root) {
     
    var len = 0;
    if (root !== null) {
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
    
    return len;
};
```

** LeetCode 地址: ** [https://leetcode.com/problems/add-digits/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
