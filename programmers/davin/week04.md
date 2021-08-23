# 4주차 알고리즘
## Maximum Depth of Binary Tree
### 문제 풀이
1. `countNode`의 인자로 `root`와 0(초기값)을 넣는다.
2. 현재 위치값을 더하기 위해 `count`를 +1 올려준다.
3. `node.left`와 `node.right`의 `count`를 구하기 위해 다시 `countNode` 함수를 실행한다.  
이때 `count` 값을 인자로 같이 넣는다.
1. `left` 또는 `right`가 `null`일 경우 `count`를 올리지 않고 리턴한다.
2. `left`와 `right`의 `count` 값을 비교하여 더 높은 숫자(더 깊은 숫자)를 반환한다.

### 제출 코드
```javascript
function countNode(node, count) {
  if (!node) {
    return count;
  }
  
  count++;

  let leftCount = countNode(node.left, count);
  let rightCount = countNode(node.right, count);

  return Math.max(leftCount, rightCount);
}

var maxDepth = function(root) {  
  return countNode(root, 0);
};
```
