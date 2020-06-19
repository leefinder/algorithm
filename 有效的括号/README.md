
## 有效的括号

- 创建栈记录上一个字符串的值，每次匹配到右括号，从栈尾取上一个值，判断是否是闭合括号，否则直接返回false
- 创建计数器，每进栈一个左括号+1，每匹配到符合的闭合右括号-1，最后只有计数器为0，说明是有效的

```
var isValid = function(s) {
    const stack = [];
    let count = 0;
    let result = true;
    for (let i of s) {
        if (i === '(') {
            count++
            stack.push(i)
        }
        if (i === '[') {
            count++
            stack.push(i)
        }
        if (i === '{') {
            count++
            stack.push(i)
        }
        if (i === ')') {
            let str = stack.pop()
            if (str !== '(') {
                result = false
                break
            } else {
                count--
            }
        }
        if (i === ']') {
            let str = stack.pop()
            if (str !== '[') {
                result = false
                break
            } else {
                count--
            }
        }
        if (i === '}') {
            let str = stack.pop()
            if (str !== '{') {
                result = false
                break
            } else {
                count--
            }
        }
    }
    return result && count === 0
};
```