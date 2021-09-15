# 7주차 알고리즘
## Merge Two Binary Trees
### 문제 풀이
1. `root1`을 베이스로 깊이 우선 탐색을 한다. `root1`의 `val`에 `root1.val` + `root2.val` 값을 할당한다.
2. 그다음, `left`를 이용하여 재귀 함수를 실행한다. `root1`의 `left`와 `root2`의 `left`를 인자로 넣어 `mergeTrees`를 실행한다.
3. `left`를 끝까지 탐색했으면, 그다음 `right`를 이용하여 재귀 함수를 실행한다. 마찬가지로 `root1`의 `right`와 `root2`의 `right`를 인자로 넣어 `mergeTrees`를 실행한다.
4. 모든 노드를 탐색한 후, `root1`을 반환한다.

### 시간 복잡도
O(n)

### 제출 코드
```javascript
var mergeTrees = function(root1, root2) {
  if (root1 === null) {
    return root2;
  }
  
  if (root2 === null) {
    return root1;
  }
  
  root1.val += root2.val;
  
  root1.left = mergeTrees(root1.left, root2.left);
  root1.right = mergeTrees(root1.right, root2.right);

  return root1;
};
```

## Merge Two Binary Trees
### 문제 풀이
1. `root.left`와 `root.right`를 바꾼다.
2. `root`의 모든 자식 요소를 반전시켜야 하기 때문에, 재귀를 이용한다. 이때, `root.left`와 `root.right`를 인자로 넣는다.
3. `root.left`를 검사하여 없다면 `null`을 반환하고, 있다면 처음과 같이 `left`와 `right`를 서로 바꾼다.

### 시간 복잡도
O(n)

### 제출 코드
```javascript
var invertTree = function(root) {
  if (!root) {
    return null;
  }

  const left = root.left;
  
  root.left = root.right;
  root.right = left;
  
  invertTree(root.left);
  invertTree(root.right);

  return root;
};
```
