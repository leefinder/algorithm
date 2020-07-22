## 二叉树中的最大路径和

> 给定一个非空二叉树，返回其最大路径和。

> 本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6

输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```

```
var maxPathSum = function(root) {
    let max = Number.MIN_SAFE_INTEGER;
    var maxPathSumHelp = function (root) {
        if (root) {
            let left = Math.max(0, maxPathSumHelp(root.left))
            let right = Math.max(0, maxPathSumHelp(root.right))
            max = Math.max(max, root.val + left + right)
            return root.val + Math.max(left, right)
        } else {
            return 0
        }
    }
    maxPathSumHelp(root)
    return max
};
```
