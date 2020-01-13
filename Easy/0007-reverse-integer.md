# [7. Reverse Integer](https://leetcode-cn.com/problems/reverse-integer/)

## Submissions

### 1st

```js
// 2019-11-12

/**
 * @param {number} x
 * @return {number}
 */
var reverse = function (x) {
  let result;

  result = reverseString(`${Math.abs(x)}`);
  if (x >= 0) {
    result = +result;
  } else {
    result = -result;
  }

  if (result < -Math.pow(2, 31) || result > (Math.pow(2, 31) - 1)) {
    return 0;
  } else {
    return result;
  }
};

var reverseString = function (str) {
  let result = '';
  for (let i = 0; i < str.length; i++) {
    result += str.charAt(str.length - 1 - i);
  }
  return result;
}

```

### 总结

如果直接使用上下限，可节省了几毫秒的用时。

又看了一个如下的范例。

```js
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let str = JSON.stringify(x);
    let num = str.length - 1;
    let arr = str.split('');
    let answer = '';
    for(num; num >= 0; num--){
        answer += arr[num];
    }
    if(x < 0){
        answer = '-' + answer.slice(0,-1)
    }
    answer = parseInt(answer);
    if(answer > 2147483647 || answer < -2147483648){
        return 0;
    }else{
        return answer;
    }
}
```

学到了 `str.split('')` 分割字符串和 `array.slice(0, -1)` 来去除最后一个元素（字符串同理）的骚操作，还有就是直接算出了上下限来提升性能。
