## BFS/DFS 1번 문제

**LeetCode | Merge Two Binary Trees**  
https://leetcode.com/problems/merge-two-binary-trees/

### 코드

```javascript
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
	if (root1 === null) return root2;
	if (root2 === null) return root1;

	root1.val += root2.val;
	root1.left = mergeTrees(root1.left, root2.left);
	root1.right = mergeTrees(root1.right, root2.right);
	return root1;
};
```

### 문제풀이

DFS) 재귀함수로 구현

### 시간복잡도

---

## BFS/DFS 2번 문제

**LeetCode | Invert Binary Tree**  
https://leetcode.com/problems/invert-binary-tree/

### 코드

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function (root) {
	if (root) {
		let temp = root.left;
		root.left = root.right;
		root.right = temp;

		invertTree(root.left);
		invertTree(root.right);
	}

	return root;
};
```

### 문제풀이

DFS) 재귀함수로 구현

### 시간복잡도

---

## 백트래킹(Backtracking) 1번 문제

**LeetCode | Maximum Number of Balloons**  
https://leetcode.com/explore/challenge/card/september-leetcoding-challenge-2021/637/week-2-september-8th-september-14th/3973/

### 코드

```javascript
/**
 * @param {string} text
 * @return {number}
 */
var maxNumberOfBalloons = function (text) {
	let obj = {
		b: 0,
		a: 0,
		l: 0,
		o: 0,
		n: 0,
	};
	const textArr = text.split("");

	textArr.forEach((el) => {
		if (obj[el] !== undefined) obj[el] += 1;
	});

	obj["o"] = Math.floor(obj["o"] / 2);
	obj["l"] = Math.floor(obj["l"] / 2);

	return Math.min.apply(null, Object.values(obj));
};
```

### 문제풀이

### 시간복잡도

**O(n)**

---

## 백트래킹(Backtracking) 2번 문제

**LeetCode | Sum of All Subset XOR Totals**  
https://leetcode.com/problems/sum-of-all-subset-xor-totals/

### 코드

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var subsetXORSum = function (nums) {
	let bits = 0;

	for (let i = 0; i < nums.length; i++) bits |= nums[i];

	let result = bits * Math.pow(2, nums.length - 1);

	return result;
};
```

### 문제풀이

### 시간복잡도
