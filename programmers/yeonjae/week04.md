# Week04

## 트리(Tree)



- 트리는 순환구조를 갖지 않는 그래프이다.
- 트리는 재귀적인 성질을 가지고있다.

------

## 이진 트리 (Binary search Tree)

- 모든 노드의 차수가 2 이하인 경우, 이진트리라고 부른다.

![](https://devmjun.github.io/img/posts/TreeType.png)

- Full binary tree : 모든 노드가 0개 또는 2개의 자식노드를 갖는다.
- Complete binary tree : 마지막 레벨을 제외하고 모든 레벨이 완전히 채워져있으며, 마지막 레벨의 가장 왼쪽 노드부터 채워져있다.
- Perfect binary tree : 모든 노드가 2개의 자식 노드를 가지고, 모든 리프노드가 동일한 깊이, 레벨을 갖는다.

----

- 문제 : [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */

var maxDepth = function(root) {
    if (!root) return 0;
    const queue = [root];
    let depth = 0;
    while (queue.length !== 0) {
        depth++;
        const len = queue.length;
        console.log(len)
        for (let i = 0; i < len; i++) {
            if (queue[i].left) queue.push(queue[i].left);                   
            if (queue[i].right) queue.push(queue[i].right);
            console.log(queue[i],queue[i].left, queue[i].right)
        }
        queue.splice(0, len);
        
    }
    return depth;
};
```

- 풀이내용 :

  - 맨 처음 루트 노드에서부터 하위 트리를 확인하면서 depth를 하나씩 증가시킨다.
    - 여기서 left, right 메서드는 각 노드별 자식을 리턴해준다.
    - Ex: [[3,9,20,null,null,15,17]].left의 경우, 전체 트리의 왼쪽 서브트리를 리턴한다.
  - queue = 0이 될 때 까지 반복문을 시행하면서 각 계층별로 왼쪽, 오른쪽 자식이 있는지 확인한다.
  - 만약 자식이 있다면 queue에 push한다.
  - 기존의 요소는 삭제한다.
  - 그림으로 while문 내의 상황을 나타내면 아래와 같다.

  <img src="https://github.com/jsalgorithm/algorithm/blob/main/programmers/1mg/KakaoTalk_Photo_2021-08-28-00-26-39.jpeg?raw=true" style="zoom: 33%;" />

  ----

- 문제 : [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

```javascript
const diameterOfBinaryTree = function (root) {
	if (!root) return 0;
	let longest = 0;
	const dfs = function (node) {
		// 왼쪽, 오른쪽의 각 리프노드까지 탐색한다.
		if (!node) return 0;

		let left = dfs(node.left);
		let right = dfs(node.right);

		longest = Math.max(longest, left + right);
		// 상태값 반환
		return Math.max(left, right) + 1;
	};
	dfs(root);
	return longest;
};
```

- 풀이내용 :
  - left, rigth 메서드는 각각 왼쪽, 오른쪽 하위 노드를 리턴한다.
  - 왼쪽 서브트리와 오른쪽 서브트리를 재귀적으로 탐색한다.
  - 재귀하면서 각각의 트리 내에서 오른쪽, 왼쪽 하위트리 중 더 긴 부분에서 거리값(1)을 리턴한다.
  - longest에는 재귀하면서 구한 오른쪽, 왼쪽 하위트리 합의 누적값 중 가장 큰 값이 저장된다.
  - 재귀가 종료될 때, 최종 longest값을 리턴한다.

-----

## 힙 (Heap)

- 힙은 ` 부모 노드는 항상 자식보다 작거나 같다 ` 혹은 ` 부모노드는 항상 자식보다 크거나 같다 ` 의 조건을 만족하는 거의 완전 트리인 트리기반의 자료구조이다.

- 부모와 자식노드간의 정의만 있을 뿐, 좌,우 간의 정의는 없기 때문에 정렬된 구조는 아니다.
- 항상 균형을 유지하는 특성을 갖고있다.
- 힙은 O(1)의 시간복잡도로 가장 큰/작은 값을 얻는데 사용된다.
  - 선형 자료구조인 Linked list / array 는 O(n)
  - 비선형 자료구조인 Binary search tree는 (log n)
- 삽입, 삭제 O(log n)
- 실제 Heap이 사용되는 경우
  - O/S의 스케쥴링 잡
  - 생산자-소비자 모델에서 소비자가 우선순위의 자원에 접근하게 함
  - 응용프로그램 내에서 최단경로(다익스트라 알고리즘)를 찾기

| 부모노드 인덱스 | 자식노드 Index |        |
| --------------- | -------------- | ------ |
| 0               | 1              | 2      |
| 1               | 3              | 4      |
| 2               | 5              | 6      |
| i               | 2i + 1         | 2i + 2 |

---

- 문제 : [Maximum Product of Two Elements in an Array](https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/)

```javascript
const maxProduct = function (nums) {
	nums.sort((a, b) => b - a);
	let i = nums[0];
	let j = nums[1];
	return (i - 1) * (j - 1);
};
```

- 풀이내용 :
  - 위 문제에서 요소들은 큰 순서대로 각각 i와 j가 된다.
  - 정렬 알고리즘을 이용하면 우선순위 큐를 만들 수 있다.
    - 자바스크립트의 경우 퀵소트를 사용해 평균적으로 n log n의 시간복잡도를 가지게된다.
  - 그러나 단순 정렬보다 힙정렬이 더 빠름 O(1)

-----

* 문제 : [ Last Stone Weight](https://leetcode.com/problems/last-stone-weight/)

```javascript
const lastStoneWeight = function (stones) {
	if (stones.length === 1) {
		return stones;
	} else if (stones.length === 0) {
		return 0;
	} else {
		let heavy1 = Math.max(...stones);
		stones.splice(stones.indexOf(heavy1), 1);
		let heavy2 = Math.max(...stones);
		stones.splice(stones.indexOf(heavy2), 1);
		if (heavy1 - heavy2 > 0) {
			let newStone = heavy1 - heavy2;
			stones.push(newStone);
            console.log(stones)
		}
		return lastStoneWeight(stones);
	}
};
```

- 풀이내용 :

  - math.max의 경우 단일루프를 발생시키기 때문에 O(n)의 시간복잡도를 평균적으로 가진다고 볼 수 있음.
    - https://github.com/v8/v8/blob/cd81dd6d740ff82a1abbc68615e8769bd467f91e/src/js/math.js#L78-L102

  - 따라서 위 코드도 평균적으로 O(n)의 시간복잡도를 갖게된다
