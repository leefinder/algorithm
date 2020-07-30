
## 二叉树中的列表

> 给你一棵以 root 为根的二叉树和一个 head 为第一个节点的链表。

> 如果在二叉树中，存在一条一直向下的路径，且每个点的数值恰好一一对应以 head 为首的链表中每个节点的值，那么请你返回 True ，否则返回 False 。

> 一直向下的路径的意思是：从树中某个节点开始，一直连续向下的路径。

```
输入：head = [4,2,8], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
输出：true
解释：树中蓝色的节点构成了与链表对应的子路径。
```

```
输入：head = [1,4,2,6], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
输出：true
```

```
输入：head = [1,4,2,6,8], root = [1,4,4,null,2,2,null,1,null,6,8,null,null,null,null,1,3]
输出：false
解释：二叉树中不存在一一对应链表的路径。
```


### 解析

- head链表匹配完，即存在子路径
- root为空，head不为空，即不存在子路径
- 路径可以从树的任意子节点开始
- 先从根节点开始匹配，递归匹配链表的val和树（可以是左子树，也可以是右子树，因此是或的关系）的val
- 根节点不匹配，则路径从左子树或者右子树开始，重复上面的递归

```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSubPath = function (head, root) {
    if (!head) {
        return true;
    }
    if (!root) {
        return false;
    }
    return isSubPathHelp(head, root) || isSubPath(head, root.left) || isSubPath(head, root.right)
}

var isSubPathHelp = function (head, root) {
    if (!head) {
        return true
    }
    if (!root) {
        return false
    }
    if (head.val !== root.val) {
        return false
    }
    return isSubPathHelp(head.next, root.left) || isSubPathHelp(head.next, root.right);
}
```