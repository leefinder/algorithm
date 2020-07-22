## 包含所有三种字符的子字符串数目

> 给你一个字符串 s ，它只包含三种字符 a, b 和 c 。请你返回 a，b 和 c 都 至少 出现过一次的子字符串数目。

```
输入：s = "abcabc"
输出：10
解释：包含 a，b 和 c 各至少一次的子字符串为 "abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab", "cabc" 和 "abc" (相同字符串算多次)。

```

- 时间复杂度过高没通过

```
var numberOfSubstrings = function(s) {
    let start = 0;
    let len = 3;
    const length = s.length;
    let count = 0;
    while(length - start >= 3) {
        while(start + len <= length) {
            let str = s.substr(start, len);
            if (str.includes('a') && str.includes('b') && str.includes('c')) {
                count++;
            }
            len++;
        }
        start++;
        len = 3;
    }
    return count;
};
```


```
var numberOfSubstrings = function(s) {
    let index1 = 0; // 字符串s的下标
    let index2 = 0;
    let count = 0;
    let map = {
        a: 0,
        b: 0,
        c: 0
    }
    s = s.split('');
    while (index1 < s.length) {
        map[s[index1]]++;
        while (map.a > 0 && map.b > 0 && map.c > 0) {
            count += s.length - index1; // 'abcccc'
            map[s[index2]]--;
            index2++; 
        }
        index1++;
    }
    return count;
};
```