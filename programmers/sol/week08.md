## 이진탐색트리(BST) 1번 문제

**LeetCode | Two Sum IV - Input is a BST**  
https://leetcode.com/problems/two-sum-iv-input-is-a-bst/

### 코드

```javascript
const findTarget = (root, k) => {
	let set = new Set();
	return inOrder(root, k);

	function inOrder(node, k) {
		if (!node) return false;
		if (set.has(node.val)) return true;
		set.add(k - node.val);
		return inOrder(node.left, k) || inOrder(node.right, k);
	}
};
```

### 문제풀이

1. set 객체를 생성한다.
2. 트리를 중위 순회하며 탐색한다.

- node가 없으면 false를 반환한다.
- set 객체에 node.val이 있으면 true를 반환한다.
- set 객체에 node.val이 없으면 set 객체에 k에서 node.val를 뺀 값을 추가한다.

3. 탐색한 결과를 반환한다.

### 시간복잡도

O(n)

---

## 이진탐색트리(BST) 2번 문제

**LeetCode | Minimum Distance Between BST Nodes**  
https://leetcode.com/problems/minimum-distance-between-bst-nodes/

### 코드

```javascript
const minDiffInBST = (root) => {
	let result = Infinity;
	let prev = Infinity;

	function inOrder(node) {
		if (!node) return;
		if (node.left) inOrder(node.left);
		result = Math.min(result, Math.abs(prev - node.val));
		prev = node.val;
		if (node.right) inOrder(node.right);
	}

	inOrder(root);

	return result;
};
```

### 문제풀이

🌟 이진탐색트리의 노드의 값은 왼쪽에서 오른쪽으로 갈수록 커지므로 노드 간의 최소 거리는 해당 노드와 직전 노드의 거리 또는 해당 노드와 직후 노드의 거리이다.

1. 결과값 변수인 result, 해당 노드 직전에 탐색한 노드값 변수인 prev에 Infinity를 할당한다.
2. 트리를 중위 순회하며 탐색한다.

- 현재 결과값과 직전에 탐색한 노드값에서 해당 노드값을 뺀 절대값 중 더 작은 값으로 result를 변경한다.
- 해당 노드값으로 pret를 변경한다.

3. 노드간의 차이가 가장 작은 값을 최종적으로 반환한다.

### 시간복잡도

O(n)

> [문제풀이 참고](https://ihp001.tistory.com/105)
