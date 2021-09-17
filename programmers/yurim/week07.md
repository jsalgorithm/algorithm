# 알고리즘 7주차

- 주제: BFS/DFS, 백트래킹
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/09/13 ~ 09/19

## 목차

- BFS/DFS

  - 문제 1) https://leetcode.com/problems/merge-two-binary-trees/
  - 문제 2) https://leetcode.com/problems/invert-binary-tree/

- 백트래킹
  - 문제 1) https://leetcode.com/explore/challenge/card/september-leetcoding-challenge-2021/637/week-2-september-8th-september-14th/3973/
  - 문제 2) https://leetcode.com/problems/sum-of-all-subset-xor-totals/

# BFS/DFS 문제 1 - 617. Merge Two Binary Trees

- 문제 분류: `BFS/DFS`
- 문제 출처: [Leetcode - 617. Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/133454458-283efaa4-cde2-4c14-bb6f-6fc2492760ed.png)

- 두 개의 이진 트리를 입력으로 받아 합쳐서 리턴하는 문제이다. 두 트리를 합치는 규칙 다음과 같다.
  - 두 트리를 겹칠 때 노드가 포개지는 경우 두 노드의 값을 합친다.
  - 한쪽 트리엔 노드가 없고 한쪽 트리의 그 자리에 노드가 있는 경우 노드를 추가한다.

문제에 있는 그림을 보면 이해가 쉬울 것이다.

## 풀이

- 두 트리를 깊이 우선 탐색(DFS)으로 순회하면서 두 트리를 merge한 새로운 트리를 반환한다. 깊이 우선 탐색을 돌기 위해서 재귀호출 방법을 사용했다.
- null인 노드는 `val`, `left`, `right`등의 어떤 프로퍼티도 없으므로 노드가 null인지 확인하고 프로퍼티에 접근해야함에 유의하자.

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {TreeNode}
 */
var mergeTrees = function (root1, root2) {
  // dfs // 재귀호출 이용

  if (!root1 && !root2) return null;

  const val1 = root1 ? root1.val : 0;
  const val2 = root2 ? root2.val : 0;

  const root = new TreeNode(val1 + val2);

  root.left = mergeTrees(root1 ? root1.left : null, root2 ? root2.left : null);
  root.right = mergeTrees(
    root1 ? root1.right : null,
    root2 ? root2.right : null
  );

  return root;
};
```

- 시간 복잡도: `O(n)`

![image](https://user-images.githubusercontent.com/33214449/133800107-1160bf4f-2251-4a33-bf26-bed4a3623a5c.png)

# BFS/DFS 문제 2 - 226. Invert Binary Tree

- 문제 분류: `BFS/DFS`
- 문제 출처: [Leetcode - 226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/133637515-5023d242-c70e-4b23-af39-2b6a4e720a6d.png)

- 주어진 트리를 좌우반전하여 리턴하는 문제이다.

## 풀이1(DFS)

재귀호출을 사용하여 DFS(깊이 우선 탐색) 방식으로 구현했다.

- 원본 트리 탐색 순서: 4 - 2 - 1 - 3 - 7 - 6 - 9 (전위 순회로 트리를 순회한 것과 같고 깊이 우선 탐색임을 알 수 있다.)

```js
// dfs // using Recursion
const invertTree = function (root) {
  if (!root) return null;

  const left = invertTree(root.left);
  const right = invertTree(root.right);

  root.left = right;
  root.right = left;

  return root;
};
```

- 시간 복잡도: `O(n)` (재귀 호출이 실행되는 횟수를 기준으로)

![image](https://user-images.githubusercontent.com/33214449/133738276-264a1c54-f24c-4638-bf25-d29d914a4331.png)

## 풀이2(BFS)

너비 우선 탐색(BFS)을 위해 큐와 반복문을 사용했다.

- 큐에 `root`노드를 넣는다.
- 큐가 빌 때까지 아래 과정을 반복한다.
  - 큐에서 노드를 하나 꺼낸다.
  - 꺼낸 노드가 `null`이 아니라면, 그 노드의 `left`와 `right`를 서로 바꾼다.
  - 그 노드의 바뀐 `left`, `right` 노드를 큐에 넣는다.
- 반복이 모두 완료되면 노드들이 invert된 트리를 최종 반환한다.

- 원본 트리 탐색 순서: 4 - 7 - 2 - 9 - 6 - 3 - 1 (트리의 레벨을 따라 순회하는 것을 볼 수 있다. 너비 우선 탐색에 해당한다.)

> **구조 분해 할당**
>
> `[popNode.left, popNode.right] = [popNode.right, popNode.left];`
>
> 위 코드로 노드의 left와 right값을 서로 바꿔 저장했다. (`[a, b] = [10, 20]`은 `a`에 `10`이, `b`에 `20`이 담기게 해준다.) 만약 `popNode.left = popNode.right` 후에 `popNode.right = popNode.left`를 실행했다면 `popNode.left`값이 이미 바뀌어 노드의 left와 right가 정상적으로 스위치되지 않았을 것이다.

```js
// bfs
const invertTree = function (root) {
  const queue = [root];

  while (queue.length) {
    const popNode = queue.shift();

    if (popNode) {
      [popNode.left, popNode.right] = [popNode.right, popNode.left];
      queue.push(popNode.left, popNode.right);
    }
  }
  return root;
};
```

- 시간 복잡도: `O(n)`
  - `while` 반복문이 큐에 데이터가 없을 때까지 반복된다. 매 반복마다 큐에서 하나씩 데이터를 꺼낸다. 큐에는 트리의 노드 개수 + 단말노드일 경우 왼쪽, 오른쪽 자식인 null도 큐에 들어간다. null이 들어가는 경우는 n이 커지면 무시 가능한 계수나 상수이므로 최종 시간 복잡도는 노드의 개수를 고려한 `O(n)`이 된다.

![image](https://user-images.githubusercontent.com/33214449/133737704-02aca4e8-1d0b-4979-a68f-3a346cac75df.png)

# 백트래킹 문제 1 - 1189. Maximum Number of Balloons

- 문제 분류: `백트래킹`
- 문제 출처: [Leetcode - 1189. Maximum Number of Balloons](https://leetcode.com/problems/maximum-number-of-balloons/)
- 라벨: `Easy`, `JavaScript`

## 문제

- 입력: 문자열 `text`
- 출력: 문자열에 `ballon`이라는 단어가 몇번 나타나는지 리턴하기(입력으로 주어진 문자열의 각 문자들은 한번만 쓸 수 있다.)

## 풀이

```js
var maxNumberOfBalloons = function (text) {
  const obj = {
    b: 0,
    a: 0,
    l: 0,
    o: 0,
    n: 0,
  };

  for (t of text) {
    obj[t]++;
  }

  return Math.floor(
    Math.min(obj['b'], obj['a'], obj['l'] / 2, obj['o'] / 2, obj['n'])
  );
};
```

- 시간 복잡도: `O(n)` (입력으로 들어온 문자열의 길이만큼 반복한다.)

![image](https://user-images.githubusercontent.com/33214449/133793321-a918b03b-bf04-44b7-a103-3c0f1928a9f2.png)

## Ref

- [Leetcode Discuss](<https://leetcode.com/problems/maximum-number-of-balloons/discuss/948621/Simple-solution-(JS)>)

# 백트래킹 문제 2 - 1863. Sum of All Subset XOR Totals

- 문제 분류: `백트래킹`
- 문제 출처: [Leetcode - 1863. Sum of All Subset XOR Totals](https://leetcode.com/problems/sum-of-all-subset-xor-totals/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/133768105-e27b022a-d38b-4512-a504-6058b6d87b13.png)

- 주어진 `nums` 배열의 부분집합(subset)을 구하고 그 부분집합의 원소들을 XOR 연산한 값을 모두 더하여 리턴하라.
- 부분집합에 따라 다음과 같이 연산할 것
  - 빈 부분집합일 경우 0
  - 부분집합의 원소가 하나일 경우 `[a]`의 XOR의 합은 `a`
  - 부분집합의 원소가 둘 이상인 경우 `[a,b,c]`의 XOR 합은 `a XOR b XOR c`

## 풀이

```js
var subsetXORSum = function (nums) {
  let sum = 0;

  function getAns(a, i, cur) {
    if (i === a.length) {
      sum += cur;
      return;
    }

    getAns(a, i + 1, cur ^ a[i]);
    getAns(a, i + 1, cur);
  }

  getAns(nums, 0, 0);
  return sum;
};
```

- 시간 복잡도:

![image](https://user-images.githubusercontent.com/33214449/133767873-fa9bcad6-db75-422a-bc9e-415fa42df930.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/sum-of-all-subset-xor-totals/discuss/1222099/C%2B%2B-0msBacktrackingVery-Much-simple-to-understand.) c++ 솔루션, 백트래킹 - 코드 참고
- [Leetcode Discuss](https://leetcode.com/problems/sum-of-all-subset-xor-totals/discuss/1236661/javascript-or-backtracking) 자바스크립트 솔루션, 백트래킹
