# 螺旋矩阵

```
const set = new Set(); // 如果当前节点访问过就不再访问

const direction = [
    [0, 1], // 列加1
    [1, 0], // 行加1
    [0, -1], // 行减1
    [-1, 0] // 列减1
]
const spiralOrder = function (matrix) {
    const m = matrix.length;
    const n = matrix[0].length;

    if (!m || !n) {
        return []
    }
    let row = 0;
    let col = 0;
    let result = [];
    let dirIndex = 0;
    for (let step = 0; step < m * n; ++step) {
        result.push(matrix[row][col]);
        set.add(`${row}-${col}`);
        let nrow = row + direction[dirIndex][0];
        let ncol = col + direction[dirIndex][1];
        if (!set.has(`${nrow}-${ncol}`)
            && nrow >= 0
            && nrow < m
            && ncol >= 0
            && ncol < n) {
            row = nrow;
            col = ncol;
        } else {
            dirIndex = (dirIndex + 1) % 4;
            row = row + direction[dirIndex][0];
            col = col + direction[dirIndex][1];
        }
    }
    return result;
}
```