## 이분탐색(Binary search) 1번 문제

**LeetCode | Intersection of Two Arrays II**  
[문제링크](leetcode.com/problems/intersection-of-two-arrays-ii)

### 시간복잡도

**O(n)**

### 코드

```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
const intersect = (nums1, nums2) => {
	let result = [];
	for (let i = 0; i < nums1.length; i++) {
		if (nums2.includes(nums1[i])) {
			result.push(nums1[i]);
			nums2.splice(nums2.indexOf(nums1[i]), 1);
		}
	}
	return result;
};
```

## 이분탐색(Binary search) 2번 문제

**LeetCode | Find the Duplicate Number**  
[문제링크](leetcode.com/problems/find-the-duplicate-number)

### 문제풀이

### 시간복잡도

방법 1 : **O(n)**
방법 2 : **O(log n)**

### 코드

- 방법 1

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findDuplicate = function (nums) {
	let arr = [];
	for (let i = 0; i < nums.length; i++) {
		if (!arr.includes(nums[i])) {
			arr.push(nums[i]);
		} else return nums[i];
	}
};
```

- 방법 2 : 이분탐색 활용

```javascript
var findDuplicate = function (nums) {
	const sorted = nums.sort();
	let left = 1;
	let right = sorted.length - 1;

	while (left < right) {
		let mid = left + Math.floor((right - left) / 2);
		let count = 0;

		for (let i = 0; i < sorted.length; i++) {
			if (sorted[i] <= mid) count++;
		}

		if (count > mid) right = mid;
		else left = mid + 1;
	}
	return left;
};
```

## 해시(hash) 1번 문제

**Programmers | 완주하지 못한 선수**

[문제링크](programmers.co.kr/learn/courses/30/lessons/42576)

### 문제풀이

❗️참고: Object VS Map

### 시간복잡도

**O(1)**

### 코드

```javascript
function solution(participant, completion) {
	const hash = new Map();

	participant.forEach((person) => {
		if (!hash.get(person)) hash.set(person, 1);
		else hash.set(person, hash.get(person) + 1);
	});

	completion.forEach((person) => {
		if (hash.get(person)) hash.set(person, hash.get(person) - 1);
	});

	for (const [key, value] of hash) {
		if (value > 0) return key;
	}
}
```

## 해시(hash) 2번 문제

**Programmers | 위장**  
[문제링크](programmers.co.kr/learn/courses/30/lessons/42578)

### 문제풀이

### 시간복잡도

### 코드

```javascript
function solution(clothes) {
	let answer = 1;
	let hash = new Map();

	for (let [key, value] of clothes) {
		hash.has(value) ? hash.set(value, hash.get(value) + 1) : hash.set(value, 1);
	}

	for (let val of hash.values()) {
		answer *= val + 1;
	}

	return answer - 1;
}
```
