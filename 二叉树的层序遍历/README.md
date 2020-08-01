## 二叉树的层序遍历

> 给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

```
示例：
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]
```

### 解析1

```
var levelOrder = function(root) {
    // 创建队列按层次存子树
    let quque = [];
    // 记录每层的子树值
    let target = [];
    // 记录当前层的节点数
    let nums = 1;
    // 记录当前层子节点个数
    let childNums = 0;
    // 记录层次并返回
    let result = [];
    if (root) {
        // 根节点进入队列
        quque.push(root);
        while (quque.length) {
            // 根节点出队
            let tree = quque.shift();
            const { left, right } = tree;
            // 如果有左子树，左子树入队
            if (left) {
                quque.push(left);
                childNums++;
            }
            // 如果有右子树，右子树入队
            if (right) {
                quque.push(right);
                childNums++;
            }
            // 记录树的val
            target.push(tree.val);
            // 每记录一次树，当前层nums减1
            nums--;
            // 当前层节点全部记录完
            if (nums === 0) {
                // 把子树个数赋值给nums，即下一层的个数
                nums = childNums;
                // 清零
                childNums = 0;
                // 记录当前层
                result.push(target);
                target = [];
            }
        }
    }
    return result;
}
```

### 解析2

```
var levelOrder = function(root) {
    const ret = [];
    if (!root) return ret;

    const q = [];
    q.push(root);
    while (q.length !== 0) {
        // 当前层的子节点个数
        const currentLevelSize = q.length;
        ret.push([]);
        for (let i = 0; i < currentLevelSize; i++) {
            const node = q.shift();
            ret[ret.length - 1].push(node.val);
            if (node.left) q.push(node.left);
            if (node.right) q.push(node.right);
        }
    }
        
    return ret;
};
```