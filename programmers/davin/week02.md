# 2주차 알고리즘
## Intersection of Two Arrays II
### 문제 풀이
1. 첫 번째 인자 `nums1`을 순회하면서 `i` 번째 요소가 `nums2`에 있는지 확인한다.
2. 만약 같은 요소가 `nums2`에 있다면 해당 요소를 `result` 배열에 추가하고,
`nums2`에서 해당 요소를 삭제한다.
3. 반복문을 마친 후 `result` 배열을 리턴한다.

### 시간 복잡도
반복문 안에서 `indexOf` 메서드를 사용하므로 O(n2)

### 제출 코드
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

## Find the Duplicate Number
### 문제 풀이
1. `nums` 배열을 순회하면서 `indexOf`를 이용하여 `i` 번째 요소의 첫 번째 인덱스를 구한다.
2. `i`와 `firstIndex`의 값이 다를 경우 `i` 번째 요소를 리턴한다.

### 시간 복잡도
반복문 안에서 `indexOf` 메서드를 사용하므로 O(n2)

### 제출 코드
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
