# 4주차 알고리즘
## Maximum Depth of Binary Tree
### 문제 풀이
1. `countNode`의 인자로 `root`와 0(초기값)을 넣는다.
2. 현재 깊이 값을 더하기 위해 `count`를 +1 올려준다.
3. `node.left`와 `node.right`의 깊이를 구하기 위해 다시 `countNode` 함수를 실행한다.  
이때 깊이 값을 인자로 같이 넣는다.
4. 들어온 `node`가 `null`일 경우 깊이 값을 올리지 않고 리턴한다.
5. `left`와 `right`의 깊이 값을 비교하여 더 높은 숫자(더 깊은 숫자)를 반환한다.

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

## Diameter of Binary Tree
### 문제 풀이
1. `countNode`의 인자로 `root`를 넣는다.
2. `node.left`와 `node.right`의 깊이를 구하기 위해 다시 `countNode` 함수를 실행한다.
3. `node`가 `null`일 경우 깊이가 없는 것이므로 0을 반환한다.
4. `left`와 `right`의 깊이를 알아낸 후, 전역변수 `count`와 `left` + `right`를 비교하여 더 큰 값을 `count`에 할당한다. (`count`는 실제 깊이를 계산하는 값, 비교하는 이유는 아래에 기재)
5. `left`와 `right`를 비교하여 더 깊이가 깊은 쪽 + 1 값을 반환한다.  
   (+ 1을 하는 이유는 현재의 깊이를 더해주어야 하기 때문에)
```
트리의 지름 = 가장 멀리 떨어져 있는 두 노드의 거리
루트와 이어져야만 하는 것은 아니다.

트리의 지름을 알아내기 위해서는 왼쪽의 깊은 값(left)과 오른쪽의 깊은 값(right)을 알아낸 후 그 둘을 합친 값을 반환해야 한다.
트리를 타고 내려가면서 left와 right를 찾는다.
left와 right가 만나는 부모 노드에서 left + right를 count에 저장한다. (부모 노드에서 무조건 한 번씩 저장한다. Math.max를 이용하여 검사를 하는 이유는 부모 노드에서 지름을 계산했을 때 더 짧아지는 것을 방지하기 위해서다.)
그리고 left와 right 중 더 깊은 값 + 현재 깊이 값을 반환한다. (다음 재귀에서 사용해야 할 값)
```
![](https://blog.kakaocdn.net/dn/UywaR/btqL38F6z6C/HA9fr2d0OLCrt34wVxruIK/img.png)

### 제출 코드
```javascript
let count = 0;

function countNode(node) {
  if(node === null) {
    return 0;
  }

  const left = countNode(node.left);
  const right = countNode(node.right);

  count = Math.max(count, left + right);

  return Math.max(left, right) + 1;
}

var diameterOfBinaryTree = function(root) {
  count = 0; // 아무 의미 없음
  countNode(root);
  return count;
};
```

## Maximum Product of Two Elements in an Array
### 문제 풀이
1. 클래스로 최대 힙을 구현한다.
2. 최대 힙의 인스턴스를 만든 후 `nums` 배열을 순회하며 값을 추가한다.
3. 느슨하게 정렬된 최대 힙에서 루트 노드를 2번씩 추출한다.
4. 추출된 값에서 -1씩 빼고 곱한 값을 반환한다.

### 제출 코드
```javascript
class Heap {
  constructor() {
    this.items = [];
  }
  
  swap = (indexA, indexB) => {
    const temp = this.items[indexA];

    this.items[indexA] = this.items[indexB];
    this.items[indexB] = temp;
  };

  getLeftChildIndex = (index) => index * 2 + 1;

  getRightChildIndex = (index) => index * 2 + 2;

  getParentIndex = (index) => Math.floor((index - 1) / 2);

  getLeftChild = (index) => this.items[this.getLeftChildIndex(index)];

  getRightChild = (index) => this.items[this.getRightChildIndex(index)];

  getParent = (index) => this.items[this.getParentIndex(index)];
  
  bubbleUp = () => {
    let index = this.items.length - 1;

    while (this.getParent(index) !== undefined && this.getParent(index) < this.items[index]) {
      this.swap(index, this.getParentIndex(index));
      index = this.getParentIndex(index);
    }
  };
  
  bubbleDown = () => {
    let index = 0;
      
    while(
      this.getLeftChild(index)  !== undefined &&
      (this.getLeftChild(index) > this.items[index] || this.getRightChild(index) > this.items[index])
    ) {
      const largerIndex = this.getLeftChild(index) > this.getRightChild(index)
        ? this.getLeftChildIndex(index)
        : this.getRightChildIndex(index);
      this.swap(largerIndex, index);
      index = largerIndex;
    }
  };
  
  add = (item) => {
    this.items.push(item);
    this.bubbleUp();
  };
  
  remove = () => {
    const rootItem = this.items[0];

    this.items[0] = this.items[this.items.length - 1];
    this.items.pop();
    this.bubbleDown();
    
    return rootItem;
  };
}

var maxProduct = function(nums) {
  const heap = new Heap();
  nums.forEach((n) => heap.add(n));
  return (heap.remove() - 1) * (heap.remove() - 1);
};
```
