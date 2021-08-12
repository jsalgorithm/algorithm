# 2주차 알고리즘
## Intersection of Two Arrays II
### 문제 풀이 01
1. 첫 번째 인자 `nums1`을 순회하면서 `i` 번째 요소가 `nums2`에 있는지 확인한다.
2. 만약 같은 요소가 `nums2`에 있다면 해당 요소를 `result` 배열에 추가하고,
`nums2`에서 해당 요소를 삭제한다.
3. 반복문을 마친 후 `result` 배열을 리턴한다.

### 시간 복잡도 01
반복문 안에서 `indexOf` 메서드를 사용하므로 O(n2)

### 제출 코드 01
```javascript
var intersect = function(nums1, nums2) {
	const copy = [...nums2];
	const result = [];

	for (let i = 0; i < nums1.length; i++) {
		if (copy.includes(nums1[i])) {
			result.push(nums1[i]);
			const index = copy.indexOf(nums1[i]);
			copy.splice(index, 1);
		}
	}

	return result;
};
```

### 문제 풀이 02
1. 인자로 들어온 두 배열을 짧은 배열과 긴 배열로 구분한다.
2. 긴 배열을 순회하여 각각의 숫자와 숫자가 몇 번 나왔는지 저장한다.
```javascript
{
	// 숫자: 횟수
	4: 2,
	8: 1,
	9: 2,
}
```
3. 짧은 배열을 순회하여 해당 값이 `hashMap`에 있거나 카운트가 0 이상이면 `result`에 그 값을 저장한다. 그 후 `hashMap`에 있는 해당 값에서 1을 뺀다.
4. `result` 배열을 반환한다.

### 시간 복잡도 02
반복문 2개를 각각 돌고 있으므로 O(n)

### 제출 코드 02
```javascript
var intersect = function(nums1, nums2) {
	const shortArr = nums1.length < nums2.length ? [...nums1] : [...nums2];
	const longArr = nums1.length < nums2.length ? [...nums2] : [...nums1];
	const hashMap = longArr.reduce((acc, cur) => {
		acc[cur] ? acc[cur] += 1 : acc[cur] = 1;
		return acc;
	}, {});
	const result = [];

	shortArr.forEach((num) => {
		if (hashMap[num]) {
			hashMap[num] -= 1;
			result.push(num);
		}
	});

	return result;
};
```

***

## Find the Duplicate Number
### 문제 풀이 01
1. `nums` 배열을 순회하면서 `indexOf`를 이용하여 `i` 번째 요소의 첫 번째 인덱스를 구한다.
2. `i`와 `firstIndex`의 값이 다를 경우 `i` 번째 요소를 리턴한다.

### 시간 복잡도 01
반복문 안에서 `indexOf` 메서드를 사용하므로 O(n2)

### 제출 코드 01
```javascript
var findDuplicate = function(nums) {
	for (let i = 0; i < nums.length; i++) {
		const firstIndex = nums.indexOf(nums[i]);
		if (firstIndex !== i) {
			return nums[i];
		}
	}
};
```

### 문제 풀이 02
1. `nums` 배열을 복사한 후 정렬한다.
2. 복사한 배열을 순회하며 `i` 번째 요소와 `i` + 1번째 요소가 같은지 검사한다.  
만약 값이 같을 경우 `i` 번째 요소를 리턴한다.

### 시간 복잡도 02
반복문 2개를 각각 돌고 있으므로 O(n)

### 제출 코드 02
```javascript
var findDuplicate = function(nums) {
	const copy = [...nums].sort((a, b) => a - b);

	for (let i = 0; i < copy.length; i++) {
		if (copy[i] === copy[i + 1]) {
			return copy[i];
		}
	}
};
```

***

## 완주하지 못한 선수
### 문제 풀이
1. `participant` 배열을 순회하여 각 선수들의 이름과 카운트를 `hashMap`에 저장한다.
```javascript
{
	mislav: 2,
	stanko: 1,
	ana: 1,
}
```
2. `completion` 배열을 순회하여 `hashMap` 선수들의 카운트를 하나씩 줄인다.
3. `for in` 문을 이용하여 `hashMap`을 순회한다. 카운트가 0 이상인 경우 해당 선수의 이름을 반환한다.

### 시간 복잡도
반복문 3개를 각각 돌고 있으므로 O(n)

### 제출 코드
```javascript
function solution(participant, completion) {
	const hashMap = participant.reduce((acc, cur) => {
		acc[cur] ? acc[cur] += 1 : acc[cur] = 1;
		return acc;
	}, {});

	completion.forEach((name) => {
		hashMap[name] -= 1;
	});

	for (let i in hashMap) {
		if (hashMap[i]) {
			return i;
		}
	}
}
```

***

## 위장
### 문제 풀이
1. `reduce`를 이용하여 `hasMap`에 옷의 유형과 이름을 저장한다.
```javascript
{
  headgear: [ 'yellow_hat', 'green_turban' ],
  eyewear: [ 'blue_sunglasses' ]
}
```
2. `for in` 문을 이용하여 의상 조합의 경우의 수를 구한다.  
`count`에 해당 유형의 의상 수 + 1(해당 유형의 의상을 입지 않을 경우)를 곱한다.
3. `count` - 1(모든 유형의 의상을 입지 않을 경우)를 반환한다.

### 시간 복잡도
반복문 2개를 각각 돌고 있으므로 O(n)

### 제출 코드
```javascript
function solution(clothes) {
	const hashMap = clothes.reduce((acc, cur) => {
		const [name, type] = cur;
		acc[type] ? acc[type].push(name) : acc[type] = [name];
		return acc;
	}, {});
	let count = 1;

	for (let i in hashMap) {
		count *= hashMap[i].length + 1;
	}

	return count - 1;
}
```
