# 二叉树

## 构建二叉树

```
    function TreeNode (val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
    function Tree () {
        this.root = null;
    }
    Tree.prototype.insert = function (val) {
        const treeNode = new TreeNode(val);
        const { root } = this;
        if (!root) {
            this.root = treeNode;
            return this;
        }
        let target = root;
        let parent = null;
        while (target) {
            parent = target;
            if (val < parent.val) {
                target = parent.left;
                if (!target) {
                    parent.left = treeNode;
                    return this;
                }
            } else {
                target = parent.right;
                if (!target) {
                    parent.right = treeNode;
                    return this;
                }
            }
        }
    }
```

## 前序遍历

> 递归实现

- 判断是否存在根节点
- 访问根节点,存入result
- 递归访问根节点的左子树
- 递归访问根节点的右子树

```
// 递归
const preorderTraversal = (root, result = []) {
    if (root) {
        result.push(root.val);
        preorderTraversal(root.left, result);
        preorderTraversal(root.right, result);
    }
    return result;
}
```

> 非递归实现

- 从根节点开始访问
- 访问目标节点的值
- 左子树存入栈中,直到左子树为null
- 节点出栈,开始访问右子树,重复上述步骤

```
// 非递归
const preorderTraversal = (root) {
    const result = [];
    const stack = [];
    let target = root;
    if (root) {
        while (target || stack.length > 0) {
            while (target) {
                stack.push(target);
                result.push(target.val);
                target = target.left;
            }
            target = stack.pop();
            target = stack.right;
        }
    }
    return result;
}
```

## 中序遍历

> 递归实现

```
const inorderTraversal = function (root, result = []) {
    if (root) {
        inorderTraversal(root.left, result);
        result.push(root.val);
        inorderTraversal(root.right, result);
    }
    return result;
}
```

> 非递归实现

```
const inorderTraversal = function (root) {
    const result = [];
    const stack = [];
    let target = root;
    if (root) {
        while (target || stack.length > 0) {
            while (target) {
                stack.push(target);
                target = target.left;
            }
            target = target.pop();
            result.push(target.val);
            target = target.right;
        }
    }
    return result;
}
```
## 后序遍历

> 递归实现

```
const postorderTraversal = function (root, result = []) {
    if (root) {
        postorderTraversal(root.left, result);
        postorderTraversal(root.right, result);
        result.push(root.val);
    }
    return result;
}
```

> 非递归实现

```
const postorderTraversal = function (root) {
    let target = root;
    const stack = [];
    let last = null;
    const result = [];
    if (root) {
        while (target || stack.length > 0) {
            while (target) {
                stack.push(target);
                target = target.left;
            }
            target = stack[stack.length - 1];
            if (!target.right || target.right == last) {
                target = stack.pop();
                result.push(target.val);
                last = target;
                target = null;
            } else {
                target = target.right;
            }
        }
    }
    return result;
}
```
