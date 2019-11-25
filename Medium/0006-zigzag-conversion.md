# [6. ZigZag Conversion](https://leetcode-cn.com/problems/zigzag-conversion/)

## Submissions

### 1st

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function (s, numRows) {
  if (s.length < 2 || numRows === 1) { return s; }

  const matrix = new Array(numRows).fill('');
  matrix[0] += s.charAt(0);
  let nextPosition = [0, 1];

  for (let i = 1; i < s.length; i++) {
    const [x, y] = nextPosition;
    matrix[y] += s.charAt(i);
    if (y < numRows - 1 && isDescendTrend(x, numRows)) {
      nextPosition = [x, y + 1];
    } else {
      nextPosition = [x + 1, y - 1];
    }
  }

  return matrix.join('');
};

var isDescendTrend = function (x, numRows) {
  return x % (numRows - 1) === 0;
}
```

### 总结

1. 性能太低（二维数组）
2. 性能优化（`string` 数组）
3. 以查询代替临时变量（代替`const [x, y] = nextPosition`），发现较上次性能居然还有略微的降低
4. 当前最优解（2019-11-05）

虽然第一次提交就通过了，但是用时和内存消耗都过高了，刚开始用了最稳健的方式，使用二维数组且使用 `null` 占位，画了“真正的”的 **Z** ，提交后发现效率太低了，随即做了调整，使用 `string` 数组即可达成目的。
