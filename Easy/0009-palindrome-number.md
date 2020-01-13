# [9. Palindrome Number](https://leetcode-cn.com/problems/palindrome-number/)

## Submissions

### 1st

```js
// 2019-12-30

/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  if (x >= 0 && x === Number(`${x}`.split('').reverse().join(''))) { return true; }
  return false;
};
```

### 总结

前两次失败的提交都是因为对 `split` 函数的错用：未传入参数，导致未分割字符串，直接得到一个元素的数组。
