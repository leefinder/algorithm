## 最大二叉树

> 给定一个不含重复元素的整数数组。一个以此数组构建的最大二叉树定义如下：

1. 二叉树的根是数组中的最大元素。
2. 左子树是通过数组中最大值左边部分构造出的最大二叉树。
3. 右子树是通过数组中最大值右边部分构造出的最大二叉树。

> 通过给定的数组构建最大二叉树，并且输出这个树的根节点。

```
var constructMaximumBinaryTree = function(nums) {
    return constructMaximumBinaryTreeHelp(nums, 0, nums.length);
};

var constructMaximumBinaryTreeHelp = function (nums, start, end) {
    if (start === end) {
        return null;
    }
    // 从闭开区间中找到最大值index
    let max = getMax(nums, start, end);
    // 最大值为根节点
    let root = new TreeNode(nums[max]);
    // 最大值左边的创建左子树
    root.left = constructMaximumBinaryTreeHelp(nums, start, max);
    // 最大值右边的创建右子树
    root.right = constructMaximumBinaryTreeHelp(nums, max + 1, end);
    return root
}
var getMax = function (nums, start, end) {
    let max = start;
    for (let i = start; i < end; i++) {
        if (nums[max] < nums[i]) {
            max = i;
        }
    }
    return max;
}
```

```
var findMax = function (nums) {
    var max = -Infinity
    var index = -1
    for (var i = 0; i < nums.length; i++) {
        if (nums[i] > max) {
            max = nums[i]
            index = i
        }
    }
    return {
        max,
        index
    }
}
var buildTree = function (nums) {
    let { max, index } = findMax(nums)
    let leftArr = nums.slice(0, index)
    let rightArr = nums.slice(index + 1)
    if (nums.length === 0) {
        return null
    }
    const tree = new TreeNode(max)
    tree.left = buildTree(leftArr)
    tree.right = buildTree(rightArr)
    return tree
}
var constructMaximumBinaryTree = function(nums) {
    return buildTree(nums)
};
```