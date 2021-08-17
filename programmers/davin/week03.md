# 3주차 알고리즘
## K번째수
### 문제 풀이
1. `commands` 배열을 `map`으로 순회하며 `array`에서 필요한 부분을 `slice` 한다.
2. `slice` 한 배열을 버블 정렬한다.
3. 정렬한 배열에서 `pick - 1` 요소를 반환한다.

### 시간 복잡도
반복문 안에서 버블 정렬을 하므로 O(n3)

### 제출 코드
```javascript
function bubbleSort(array) {
	const copyArray = [...array];

	for (let i = 0; i < copyArray.length - 1; i++) {
		for (let j = 0; j < copyArray.length - 1 - i; j++) {
			if (copyArray[j] > copyArray[j + 1]) {
				const temp = copyArray[j];
				copyArray[j] = copyArray[j + 1];
				copyArray[j + 1] = temp;
			}
		}
	}

	return copyArray;
}

function solution(array, commands) {
	return commands.map((command) => {
		const [first, last, pick] = command;
		const sortedArray = bubbleSort(array.slice(first - 1, last));
		return sortedArray[pick - 1];
	});
}
```

## 가장 큰 수
### 문제 풀이
1. `numbers` 배열을 얕은 복사한 후 `sort` 메서드를 이용하여 정렬한다.
2. 정렬할 때 각 요소를 문자열로 변환하여 합친 후 비교한다.
```
sort((a, b) => (b + a) - (a + b))
```
3. 정렬된 배열을 `join` 하여 반환한다.  
  이때 `numbers` 배열에 0만 존재하는 경우, `'000'`을 리턴하는 것을 방지하기 위해 삼항 조건 연산자를 이용한다.

### 시간 복잡도
(Chrome, Firefox의 경우) `sort` 메서드의 시간 복잡도는 O(n log n)  
[What is Array.prototype.sort() time complexity?](https://stackoverflow.com/questions/57763205/what-is-array-prototype-sort-time-complexity)

### 제출 코드
```javascript
function solution(numbers) {
	const result = [...numbers]
		.sort((a, b) =>`${b}${a}` - `${a}${b}`)
		.join('');

	return result[0] === '0' ? '0' : result;
}
```
