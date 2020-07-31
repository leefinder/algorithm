## N叉树的层序遍历

> 给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。

> 例如，给定一个 3叉树 :

```
[1, 3, 2, 4, 5, 6]
[
     [1],
     [3,2,4],
     [5,6]
]
```

### 解析

> 迭代

1. root为空时返回空数组，不存在
2. 开始迭代，往queue队列中push根节点，记录当前队列长度
3. 逐个出队列，存在q中，直到队列为空，把出队的树的子树存在队列中进入下一个循环
```
var levelOrder = function (root) {
    let result = [];
    let queue = [];
    if (!root) {
        return result;
    }
    queue.push(root);
    while (queue.length) {
        let q = []
        let len = queue.length;
        for (let i = 0; i < len; i++) {
            const t = queue.shift();
            q.push(t.val);
            for (let j = 0; j < t.children.length; j++) {
                queue.push(t.children[j]);
            }
        }
        result.push(q);
    }
    return result;
}
```