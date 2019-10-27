# [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)

## Submissions

### 1st

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  const resultArray = [];
  let l1node = l1;
  let l2node = l2;
  const addResult = addTwoNode(l1node, l2node, 0);
  resultArray.push(addResult[0]);
  let nextCarry = addResult[1];
  while(l1node.next || l2node.next || nextCarry) {
    if (l1node.next && l2node.next) {
      l1node = l1node.next;
      l2node = l2node.next;
      const addResult = addTwoNode(l1node, l2node, nextCarry);
      resultArray.push(addResult[0]);
      nextCarry = addResult[1];
    } else if (l1node.next && !l2node.next) {
      l1node = l1node.next;
      const addResult = addTwoNode(l1node, null, nextCarry);
      resultArray.push(addResult[0]);
      nextCarry = addResult[1];
    } else if (!l1node.next && l2node.next) {
      l2node = l2node.next;
      const addResult = addTwoNode(null, l2node, nextCarry);
      resultArray.push(addResult[0]);
      nextCarry = addResult[1];
    } else if (nextCarry) {
      resultArray.push(nextCarry);
      nextCarry = 0;
    }
  }

  let resultNode = new ListNode(resultArray[0]);
  const result = resultNode;
  for(let i = 1; i < resultArray.length; i++) {
    resultNode.next = new ListNode(resultArray[i]);
    resultNode = resultNode.next;
  }
  return result;
};

var addTwoNode = function(node1, node2, carry) {
  const sum = (node1 ? node1.val : 0) + (node2 ? node2.val : 0) + carry;
  const nextCarry = Math.floor(sum / 10);
  const value = sum % 10;
  return [value, nextCarry];
}
```

#### 事后总结

还在想怎么调用 `ListNode` 才能设置 `next` 属性，该开始怎么写都是

```js
const node = ListNode(0)
```

不得已看了下资料，才发现原来要用到 `new` 啊，真是太年轻了。怎么也没想到一个函数要用到 `new` ，看来原生 JS 还得好好学习下了。
