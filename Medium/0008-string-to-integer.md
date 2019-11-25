# [8. String to Integer (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)

## Submissions

### 1st

```js
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function (str) {
  const validStr = str.trim();
  if (!validStr) { return 0 }

  const hasSymbol = validStr.startsWith('+') || validStr.startsWith('-');
  return processOverflow(convertToNum(hasSymbol ? validStr.substring(1) : validStr, validStr.startsWith('-')));
};

var convertToNum = function (str, isNegative) {
  const [numStr] = str.match(/\d*/);
  if (numStr) {
    return isNegative ? -Number(numStr) : Number(numStr);
  }
  return 0;
}

var processOverflow = function (num) {
  if (num <= -2147483648) {
    return -2147483648;
  } else if (num >= 2147483647) {
    return 2147483647;
  }
  return num;
}
```

### 总结

性能中等，参考了两个范例：

性能不错的一个:

```js
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function (str) {
  // str = str.trim()
  let number = parseInt(str)
  let max = Math.pow(2, 31) - 1
  let min = -Math.pow(2, 31)
  if (isNaN(number)) return 0;
  if (number >= max)
    number = max
  if (number <= min)
    number = min
  return number
};
```

最佳性能的一个：

```js
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function(str) {
    const result = str.trim().match(/^(-|\+)?\d+/g);
  return result
    ? Math.max(Math.min(Number(result[0]), 2 ** 31 - 1), -(2 ** 31))
    : 0;
};
```

综合了一下这两个的实现方式，得到第二次提交结果。

### 2nd

```js
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function (str) {
    let number = parseInt(str);
    if (isNaN(number)) { return 0 };
    return Math.max(Math.min(Number(number), 2147483647), -2147483648);
};
```

还是只达到了性能不错的水平，看样子用正则应该比 `parseInt` 的性能好一些。
