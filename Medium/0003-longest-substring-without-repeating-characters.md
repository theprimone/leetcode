# [3. Longest Substring Without Repeating Characters](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

这次把帐号数据迁到国内了。

## Submissions

### 1st

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  if (!s) return 0;

  let result = 1;
  let substring = s.substr(0, 1);
  for(let i = 1; i < s.length; i++) {
    substring = getNextSubstring(substring, s.substr(i, 1));
    if (substring.length > result) {
      result = substring.length;
    }
  }
  return result;
};

var getNextSubstring = function(substring, char) {
  let repeatIndex = substring.indexOf(char);
  if (repeatIndex < 0) { return substring + char }

  return substring.substring(repeatIndex + 1) + char;
}
```

#### 事后总结

[Deprecated] str.substr(start: number, length?: number)

str.substring(indexStart, indexEnd?: number)

[str.indexOf(searchValue, fromIndex?: number)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf)

说说前三次提交的问题

* 没考虑空字符串
* 发现重复的字符后直接重置为当前字符
* 发现重复的字符后未分离重复的字符
