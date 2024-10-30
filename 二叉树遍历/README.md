# 二叉树

- DFS（深度优先搜索）：沿着根节点递归下去，遇到叶子节点则向上回溯；
- BFS (广度优先搜索)：按照二叉树的层次访问，通常采用队列保存每个层次的节点。

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
- 左子树存入栈中，直到左子树为null
- 节点出栈，开始访问右子树，重复上述步骤

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
```
// 前序遍历：中左右
// 压栈顺序：右左中

var preorderTraversal = function(root, res = []) {
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
        stack.push(node); // 中
        stack.push(null);
    };
    return res;
};
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
```
//  中序遍历：左中右
//  压栈顺序：右中左
 
var inorderTraversal = function(root, res = []) {
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        if (node.right) stack.push(node.right); // 右
        stack.push(node); // 中
        stack.push(null);
        if (node.left) stack.push(node.left); // 左
    };
    return res;
};

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

> 非递归实现1

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

> 非递归实现2

- 后序遍历打印时左子树->右子树->根节点
- 反过来思考，先输入根节点->右子树->左子树，然后再反转

```
const postorderTraversal = (root) {
    const result = [];
    if (!root) {
        return result;
    }
    const stack = [root];
    while (stack.length > 0) {
        const t = stack.pop();
        result.push(t.val);
        stack.push(t.left);
        stack.push(t.right);
    }
    return result.reverse();
}

```
```
// 后续遍历：左右中
// 压栈顺序：中右左
 
var postorderTraversal = function(root, res = []) {
    const stack = [];
    if (root) stack.push(root);
    while(stack.length) {
        const node = stack.pop();
        if(!node) {
            res.push(stack.pop().val);
            continue;
        }
        stack.push(node); // 中
        stack.push(null);
        if (node.right) stack.push(node.right); // 右
        if (node.left) stack.push(node.left); // 左
    };
    return res;
};
```
