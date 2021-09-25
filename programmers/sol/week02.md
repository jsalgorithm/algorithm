## 이분탐색(Binary search) 1번 문제

**LeetCode | Intersection of Two Arrays II**  
leetcode.com/problems/intersection-of-two-arrays-ii

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

### 문제풀이

1. 비어있는 result 배열을 만든다.
2. nums1 배열에 for문으로 접근한다.
3. nums2 배열에 nums1 배열과 중복되는 값이 존재하면 앞서 선언한 result 배열에 넣는다.
4. nums2 배열에서 nums1 배열과 중복되는 값을 splice 함수로 제거한다.
5. result 배열에는 nums1 배열과 nums2 배열의 교집합인 값들이 담기게 된다.

### 시간복잡도

**O(n)**

## 이분탐색(Binary search) 2번 문제

**LeetCode | Find the Duplicate Number**  
leetcode.com/problems/find-the-duplicate-number

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

### 문제풀이

- 방법 1

1. 비어있는 arr 배열을 만든다.
2. nums 배열에 for문으로 접근한다.
3. arr 배열에 nums[i]값이 존재하지 않으면 arr 배열에 넣는다.
4. 반면 존재한다면 nums[i]값을 반환한다.
   ❗️중복되는 값이 1개일 경우에 한정됨.

- 방법 2

1. nums 배열을 sort 함수로 오름차순 정렬하고 sorted 변수에 저장한다.
2. 조건 범위가 [1, n]이므로 left 변수에 1, right 변수에 sorted 배열의 마지막 index 값을 저장한다.
3. left < right 조건을 만족할 때까지 while문을 돌린다.
4. mid 변수에 sorted 배열의 중간 값을 저장하고, count 변수를 초기화 한다.
5. sorted 배열에 for문으로 접근하여 sorted[i]값이 mid보다 작거나 같으면 count를 증가시킨다.
   => sorted[i]값이 left에 위치하면 count를 증가시킨다는 의미
6. count가 mid보다 크면 right가 mid가 된다.
   => 오른쪽 값들을 제외한다는 의미
7. 그 반대면 left가 mid+1이 된다.
   => 왼쪽 값들을 제외한다는 의미
8. left값을 반환한다.

### 시간복잡도

방법 1 : **O(n)**
방법 2 : **O(log n)**

---

## 해시(hash) 1번 문제

**Programmers | 완주하지 못한 선수**

programmers.co.kr/learn/courses/30/lessons/42576

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

### 문제풀이

1. Map 객체를 생성하고 hash 변수에 저장한다.
2. participant 배열에 forEach 함수로 접근하여 person 인자를 탐색한다.
3. hash 객체에 person 인자가 없으면 {person : 1}로 세팅한다.
4. 인자가 있으면 value값에 1을 더한다.
5. completion 배열에 forEach 함수로 접근하여 person 인자를 탐색한다.
6. hash 객체에 person 인자가 있으면 해당 인자의 value값에 1을 뺀다.
7. hash 객체에 for of문으로 접근한다.
8. value가 0보다 큰 경우, key값을 반환환다.
   => 여기서 value가 남아있는 person 인자가 완주하지 못한 선수이다.

참고: Object vs Map  
https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Keyed_collections

### 시간복잡도

**O(1)**

## 해시(hash) 2번 문제

**Programmers | 위장**  
programmers.co.kr/learn/courses/30/lessons/42578

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

### 문제풀이

1. answer 변수에 1을 저장한다.
   => 무조건 1개 이상의 의상을 입는다는 조건
2. Map 객체를 생성하고 hash 변수에 저장한다.
3. clothes 2차원 배열에 for of문으로 접근한다.
4. hash 객체에 value가 있으면 value값에 1을 더하고, 없으면 {value: 1}로 세팅한다.
5. Object.values() 메소드로 hash 객체의 value값을 담은 배열을 생성하고 for of문으로 접근하면서 answer에 (value + 1)를 곱한다.
   => 의상을 조합하는 모든 경우의 수를 계산함.
6. 모든 의상을 입지 않은 경우를 뺀 값을 반환한다.

### 시간복잡도

**O(log n)**
