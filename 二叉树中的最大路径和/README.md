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
            // 左、右子树最大和与0比较，负数舍弃
            let left = Math.max(0, maxPathSumHelp(root.left))
            let right = Math.max(0, maxPathSumHelp(root.right))
            // 尝试获取最大和
            max = Math.max(max, root.val + left + right)
            // 对于根节点最大和，根节点的值＋左右子树较大的和
            return root.val + Math.max(left, right)
        } else {
            return 0
        }
    }
    maxPathSumHelp(root)
    return max
};
```
