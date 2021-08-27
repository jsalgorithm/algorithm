# 알고리즘 4주차

- 주제: 힙, 이진트리
- 작성자: 박유림(Wol-dan) / @pul8219

## 목차

- 이진트리
  - 문제 1) [Maximum Depth of Binary Tree](#Maximum-Depth-of-Binary-Tree)
  - 문제 2) [Diameter of Binary Tree](#Diameter-of-Binary-Tree)
- 힙
  - 문제 1) [Maximum Product of Two Elements in an Array](#Maximum-Product-of-Two-Elements-in-an-Array)
  - 문제 2) [Last Stone Weight](#Last-Stone-Weight)

# Maximum Depth of Binary Tree

- 문제 분류: `이진트리`
- 문제 출처: [Leetcode - 104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- 라벨: `Easy`, `JavaScript`

## 문제

- 트리 노드 정의

어떤 TreeNode의 left, right가 또 다른 TreeNode를 가리키고 있는 식으로 트리가 구성되어있을 것이다.

```js
function TreeNode(val, left, right) {
  this.val = val === undefined ? 0 : val;
  this.left = left === undefined ? null : left;
  this.right = right === undefined ? null : right;
}
```

- 입력: 이진 트리의 root 노드
- 출력: 이 이진 트리의 최대 깊이

## 풀이 1(통과X)

- 헷갈렸던 점
  - 문제에 `root = [3,9,20,null,null,15,7]`라고 되어있는 걸 보고 입력값으로 들어오는 `root`가 배열인 줄 알고 어떻게 구현해야하나 난감했다. 알고보니 root로 들어오는 것은 트리 자체였다.(자세히 말하면 입력값은 root 노드값이다. left, rigth 속성으로 트리 전체를 따라갈 수 있음)

아래 풀이는 이 문제가 이진 트리가 아니라 왼쪽 자식은 루트보다 작고 오른쪽 자식은 루트보다 큰 `이진 탐색 트리`인줄 알고 잘못 푼 풀이이다. 트리를 레벨 순서로 순회한 뒤 가장 끝값을 찾아 해당 값을 검색하며 depth를 증가시키는 방식으로 구현했다. 문제의 트리가 이진 탐색 트리 였더라도 이렇게까지 구현하지 않아도 됐을텐데 생각을 너무 복잡하게 했다.

```js
var levelTraversal = function (node) {
  if (node === null) {
    // == vs ===
    return;
  }
  let queue = [];
  queue.push(node);
  let pop_node;
  while (queue.length > 0) {
    pop_node = queue.shift();
    if (pop_node.left) queue.push(pop_node.left);
    if (pop_node.right) queue.push(pop_node.right);
  }
  return pop_node;
};

var maxDepth = function (root) {
  if (root == null) return 0;

  let count = 0;

  var search = function (val, node) {
    count++;
    if (node == null || node.val === val) return node;
    else if (val < node.val) return search(val, node.left);
    else return search(val, node.right);
  };

  // 레벨 순회
  const target = levelTraversal(root);

  // 레벨 순회 후 가장 뒤에 있는 요소를 검색하며 카운트값 증가시킴
  search(target.val, root);
  return count;
};
```

## 풀이 2(재귀)

파라미터로 `depth`값을 주고 왼쪽 서브트리와 오른쪽 서브트리에 `searchDepth`함수를 재귀적으로 적용했다. 노드가 `null`인 경우에는 파라미터로 받은 `depth`를 그대로 리턴하기 때문에 `depth`값에 변화가 없다.

```js
const searchDepth = (node, depth) => {
  if (node === null) return depth;
  depth++;

  const leftDepth = searchDepth(node.left, depth);
  const rightDepth = searchDepth(node.right, depth);

  const max = Math.max(leftDepth, rightDepth);
  return max;
};

const maxDepth = (root) => {
  return searchDepth(root, 0);
};
```

- 시간 복잡도: O(N)
  - 노드의 개수만큼 로직이 이루어질 것 같아서
  - ❓ 재귀함수로 문제를 푼 경우 시간 복잡도를 어떻게 계산해야할까?

![image](https://user-images.githubusercontent.com/33214449/131151977-4a26e792-d8e3-44af-bf07-92a3f51d13b6.png)

## 다른 풀이들(참고하기)

- 재귀적인 방법(recursive)

풀이 2보다 코드가 굉장히 간단하다.

```js
var maxDepth = function (root) {
  if (root === undefined || root === null) {
    return 0;
  }
  return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
};
```

다음과 같은 트리에서

![image](https://user-images.githubusercontent.com/33214449/131168175-238ad2dc-5903-411c-8479-5536c929c584.png)

아래 사진처럼 재귀함수가 리턴되며 코드가 실행된다.

![image](https://user-images.githubusercontent.com/33214449/131168137-8424a947-178e-4f62-bb17-7a1e8a552893.png)

---

- 반복을 이용한 방법

노드를 큐에 삽입하고 제거하며 `depth`값을 변경하는 방식을 사용한 코드이다.

```js
var maxDepth = function (root) {
  if (!root) return 0;
  const queue = [root];
  let depth = 0;
  while (queue.length !== 0) {
    depth++;
    const len = queue.length;
    for (let i = 0; i < len; i++) {
      if (queue[i].left) queue.push(queue[i].left);
      if (queue[i].right) queue.push(queue[i].right);
    }
    queue.splice(0, len);
  }
  return depth;
};
```

## Ref

- [[LeetCode] 104. Maximum Depth of Binary Tree](https://velog.io/@lucid/LeetCode-104.-Maximum-Depth-of-Binary-Tree)
- [Leetcode Discussion](https://leetcode.com/problems/maximum-depth-of-binary-tree/discuss/279066/Two-easy-solution-using-JavaScript)
- [[LeetCode] Maximum Depth of Binary Tree (JS)](https://velog.io/@gyu716625/LeetCode-Maximum-Depth-of-Binary-Tree-JS#%ED%95%B4%EA%B2%B0%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

# Last Stone Weight

- 문제 분류: `이진트리`
- 문제 출처: [Leetcode - 1046. Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)
- 라벨: `Easy`, `JavaScript`

## 문제

- `stones` 배열의 원소 각각은 돌의 무게를 의미한다.
- 가장 무거운 2개의 돌을 찾아서(단 두 개의 돌을 `x`, `y`라고 가정할 때 `x <= y`)
  - `x==y`일 경우, 배열에서 두 개의 돌 모두 삭제한다.
  - `x!=y`일 경우, `x`인 돌은 배열에서 삭제하고 `y`는 `y-x` 무게로 바꾼다.
- 위 과정을 배열에 돌이 1개 남을 때까지 계속한다.
- 마지막에 남은 돌의 무게를 리턴하고, 만약 남은 돌이 없다면 `0`을 리턴하도록 하자.

## 풀이 1

- 이진 트리 개념을 적용하지 못했다.

```js
var lastStoneWeight = function (stones) {
  let size = stones.length;

  while (size >= 2) {
    stones.sort((a, b) => {
      return a - b;
    });

    x = stones.pop();
    y = stones.pop();

    if (x == y) {
      size -= 2;
    } else {
      size -= 1;
      stones.unshift(x - y);
    }
  }

  return stones.length === 0 ? 0 : stones[0];
};
```

- 시간 복잡도: O(n^2) 이상

![image](https://user-images.githubusercontent.com/33214449/131167403-02b7b510-5dcc-4490-bbe9-5c858bda5e22.png)

## Ref

- [Leetcode Discussion](https://leetcode.com/problems/last-stone-weight/discuss/594316/Javascript-99-time)

# Maximum Product of Two Elements in an Array

- 문제 분류: `힙`
- 문제 출처: [Leetcode - 1464. Maximum Product of Two Elements in an Array](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/)
- 라벨: `Easy`, `JavaScript`

## 문제

- 입력: 양의 정수가 담긴 배열(`nums`)
- 출력: 두 개의 서로 다른 인덱스값 `i`, `j`를 정해서 `(nums[i]-1)*(nums[j]-1)`의 최대값을 리턴하기

## 풀이 1

가장 큰 `(nums[i]-1)*(nums[j]-1)`값을 리턴하려면, `nums[i]`와 `nums[j]`가 배열에서 가장 큰값, 그 다음으로 큰 값 이어야 한다.

- 배열을 돌면서 배열의 원소로 최대 히프를 만듦(`insert` 함수 이용)
- 최대 히프(`heap` 배열)에서 가장 상위 노드가 최대값일 것이다. 이 값을 `numsi` 변수에 저장해둔다.
- 전 단계에서 찾았던 최대값을 제외한 나머지 원소로 배열을 만든다. 그리고 이 배열로 다시 최대 히프를 만든다.
- 이 최대 히프의 가장 상위 노드값을 `numsj` 변수에 저장해둔다.
- `(numsi-1)*(numsj-1)`값을 리턴한다.

```js
function Heap() {
  this.heap = [];
  // heap 배열에 원소를 넣으면서 최대 힙을 만든다. -> 다 만들고 나면 가장 상위 노드가 최댓값이 될 것임
  this.insert = function insert(val) {
    this.heap.push(val);
    let curIndex = this.heap.length - 1;
    let parentIndex = Math.floor((curIndex - 1) / 2);

    while (this.heap[parentIndex] < val) {
      [this.heap[parentIndex], this.heap[curIndex]] = [
        this.heap[curIndex],
        this.heap[parentIndex],
      ];
      curIndex = parentIndex;
      parentIndex = Math.floor((curIndex - 1) / 2);
    }
  };
}

var maxProduct = function (nums) {
  const obj = new Heap();

  // nums[i]에 올 값 구하기(가장 큰 값)
  for (let i = 0; i < nums.length; i++) {
    obj.insert(nums[i]);
  }
  const numi = obj.heap[0];
  const newNums = obj.heap.slice(1);

  // 힙(배열) 초기화
  obj.heap = [];

  // nums[j]에 올 값 구하기(그 다음으로 큰 값)
  for (let i = 0; i < newNums.length; i++) {
    obj.insert(newNums[i]);
  }
  const numj = obj.heap[0];

  return (numi - 1) * (numj - 1);
};
```

- 시간 복잡도: O(n^2)

![image](https://user-images.githubusercontent.com/33214449/131165722-faf8104e-9c8b-4c25-8b10-690a5038bfcc.png)

## 다른 풀이들(참고하기)

- `nums` 배열을 `sort()`를 사용해 내림차순으로 정렬하고, `[0]`, `[1]` 인덱스값을 사용한 방법

```js
var maxProduct = function (nums) {
  nums.sort((a, b) => b - a);
  return (nums[0] - 1) * (nums[1] - 1);
};
```

![image](https://user-images.githubusercontent.com/33214449/131165912-75afd90d-2f34-41e1-a4b0-b41389fe6567.png)

## Ref

- [자바스크립트로 힙 (Heap) 구현하기](https://velog.io/@cada/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A1%9C-%ED%9E%99-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0#%EC%82%BD%EC%9E%85-%EB%A9%94%EC%86%8C%EB%93%9C-%EA%B5%AC%ED%98%84) 최대 히프 삽입 코드 참고

# Diameter of Binary Tree

- 문제 분류: `힙`
- 문제 출처: [Leetcode - 543. Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)
- 라벨: `Easy`, `JavaScript`
