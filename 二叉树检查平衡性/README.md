## 二叉树检查平衡性

> 实现一个函数，检查二叉树是否平衡。在这个问题中，平衡树的定义如下：任意一个节点，其两棵子树的高度差不超过 1。

```
给定二叉树 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
返回 true 。

给定二叉树 [1,2,2,3,3,null,null,4,4]
      1
     / \
    2   2
   / \
  3   3
 / \
4   4
返回 false 。

```

### 解析

```
var isBalanced = function (root) {
    // 如果根节点为null，即平衡
    if (!root) {
        return true
    }
    // 获取左子树最大深度
    const left = isBalancedHelp(root.left)
    // 获取右子树最大深度
    const right = isBalancedHelp(root.right)
    if (Math.abs(left - right) > 1) {
        return false
    }
    return isBalanced(root.left) && isBalanced(root.right)
}

var isBalancedHelp = function (root) {
    if (!root) {
        return 0
    }
    // 递归执行比较左右子树深度，获取当前树的最大深度
    return Math.max(isBalancedHelp(root.left), isBalancedHelp(root.right)) + 1
}
```