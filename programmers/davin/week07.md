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

## Invert Binary Tree
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

## Maximum Number of Balloons
### 문제 풀이
1. 인자로 받은 `text`를 배열로 변환한 `array`를 선언한다.  
   최종 카운트를 반환할 `result`도 선언한다.
2. `array`를 이용하여 `while` 문을 돈다.  
   `while` 문 내부에서 문자열 `temp`를 선언한다.
3. `balloon`을 이용하여 `for` 문을 돈다.  
   알파벳을 하나씩 짚어 `array`에 해당 알파벳이 있을 경우 `temp`에 더한다.  
   그리고 `array`에서 해당 알파벳을 삭제한다. (중복 사용을 방지하기 위함)
4. `temp`와 `balloon`이 같을 경우 `result`를 1씩 더해주고, `temp`를 초기화한다.
5. 최종적으로 `result`를 반환한다.

### 시간 복잡도
O(n2)

### 제출 코드
```javascript
var maxNumberOfBalloons = function(text) {
  const BALLOON = 'balloon';
  const array = text.split('');
  let result = 0;

  while(array.length) {
    let temp = '';
    
    for (let j = 0; j < BALLOON.length; j++) {
      const index = array.findIndex((s) => s === BALLOON[j]);

      if (index >= 0) {
        temp += array[index];
      }
      
      array.splice(index, 1);
    }
    
    if (temp === BALLOON) {
      result += 1;
      temp = '';
    }
  }
  
  return result;
};
```

## Sum of All Subset XOR Totals
### 문제 풀이
1. 인자로 받은 `nums` 배열을 이용하여 (모든 경우의) 이중 배열을 만든다.  
```
nums = [1, 3]
subsets = [[1], [3], [1, 3]]
```
2. 이중 배열 `subsets`을 `for` 문을 이용하여 순회한다.  
   `i` 번째 요소의 length가 1일 경우 그 값을 `sum`에 그대로 더한다.  
   `i` 번째 요소의 length가 1 이상일 경우 `reduce`를 이용하여 XOR 값을 구한다. 그리고 그 값을 `sum`에 더한다.
3. `sum`을 반환한다.

### 시간 복잡도
O(n log n)? O(n2)?

### 제출 코드
```javascript
var subsetXORSum = function(nums) {
  const subsets = [[]];
  let sum = 0;

  for (const num of nums) {
    const last = subsets.length - 1;

    for(let i = 0; i <= last; i++) {
      subsets.push([...subsets[i], num]);
    }
  }

  for (let i = 0; i < subsets.length; i++){
    if (subsets[i].length === 1) {
      sum += parseInt(subsets[i]);
    }
    
    if (subsets[i].length > 1) {
      sum += parseInt(subsets[i].reduce((acc,cur) => acc ^ cur));   
    }
  }

  return sum
};
```
