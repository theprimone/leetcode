# [5. Longest Palindromic Substring](https://leetcode-cn.com/problems/longest-palindromic-substring/)

## Submissions

### 1st

```js
// 2019-10-30

/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  if (s.length <= 1) {
    return s;
  }

  for (let range = s.length; range >= 2; range--) {
    for (let startIndex = 0; startIndex <= s.length - range; startIndex++) {
      const substring = s.substring(startIndex, startIndex + range);
      if (isPalindrome(substring)) {
        return substring;
      }
    }
  }
  return s.substring(0, 1);
};

var isPalindrome = function (s) {
  for (let i = 0; i < Math.floor(s.length / 2); i++) {
    if (s.charAt(i) !== s.charAt(s.length - 1 - i)) {
      return false;
    }
  }
  return true;
}
```

### 总结

前三次提交的问题

1. 没考虑单个字符
2. 未找到回文子串时，应返回单个字符，不应返回整个字符串
3. [超出时间限制](https://leetcode-cn.com/submissions/detail/34937017/)。将后半部分字符串反向（使用 `substring` 去取单个字符）后再与前半部分对比，测试 `"azwdzwmwcqzgcobeeiphemqbjtxzwkhiqpbrprocbppbxrnsxnwgikiaqutwpftbiinlnpyqstkiqzbggcsdzzjbrkfmhgtnbujzszxsycmvipjtktpebaafycngqasbbhxaeawwmkjcziybxowkaibqnndcjbsoehtamhspnidjylyisiaewmypfyiqtwlmejkpzlieolfdjnxntonnzfgcqlcfpoxcwqctalwrgwhvqvtrpwemxhirpgizjffqgntsmvzldpjfijdncexbwtxnmbnoykxshkqbounzrewkpqjxocvaufnhunsmsazgibxedtopnccriwcfzeomsrrangufkjfzipkmwfbmkarnyyrgdsooosgqlkzvorrrsaveuoxjeajvbdpgxlcrtqomliphnlehgrzgwujogxteyulphhuhwyoyvcxqatfkboahfqhjgujcaapoyqtsdqfwnijlkknuralezqmcryvkankszmzpgqutojoyzsnyfwsyeqqzrlhzbc"` 时用时 256ms 左右，改为 `charAt` 的方式取单个字符用时 215ms 左右。第一次通过的测试用时 70ms 左右。
