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
