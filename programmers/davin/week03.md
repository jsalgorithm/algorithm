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

## 모의고사
### 문제 풀이 01
1. 수포자 1, 수포자 2, 수포자 3의 답안 패턴을 하나의 배열에 넣어 2차원 배열을 만들고 반복문을 돌린다.
2. 그 안에서 `answers` 배열의 반복문을 돌린다. 패턴의 답과 `answer`가 일치하면 `scores`에서 해당 사람의 스코어를 올린다.
3. 반복문을 끝까지 돈 후, `scores`에서 가장 높은 점수를 구한다.
4. 가장 높은 점수와 본인의 점수가 일치하는 사람들의 배열을 반환한다.

### 시간 복잡도 01
2중 for 문을 돌리고 있으므로 O(n^2)

### 제출 코드 01
```javascript
function solution(answers) {
	const scores = { 1: 0, 2: 0, 3: 0 };
	const patterns = [
		[1, 2, 3, 4, 5],
		[2, 1, 2, 3, 2, 4, 2, 5],
		[3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
	];

	patterns.forEach((pattern, patternIndex) => {
		let index = 0;

		answers.forEach((answer) => {
			if (!pattern[index]) {
				index = 0;
			}

			if (pattern[index] === answer) {
				scores[patternIndex + 1]++;
			}

			index++;
		});
	});

	const maxScore = Math.max(...Object.values(scores));

	return Object.keys(scores).reduce((acc, cur) => {
		if (scores[cur] === maxScore) {
			acc.push(Number(cur));
		}
		return acc;
	}, []);
}
```

### 문제 풀이 02
1. `answers` 배열에 대한 반복문을 돈다.
2. 반복문을 돌면서 답안이 수포자 1, 수포자 2, 수포자 3의 패턴과 맞는지 확인한다.
3. `scores` 배열에서 최댓값을 구한다. (최고 점수)
4. `reduce`를 이용해서 최고 점수와 일치하는 요소의 인덱스를 `acc`에 `push` 한다.
### 시간 복잡도 02
O(n)

### 제출 코드 02
```javascript
function solution(answers) {
	const scores = [0, 0, 0];
	const first = [1, 2, 3, 4, 5];
	const second = [2, 1, 2, 3, 2, 4, 2, 5];
	const third = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

	for (let i = 0; i < answers.length; i++) {
		if (first[i % first.length] === answers[i]) {
			scores[0]++;
		}
		if (second[i % second.length] === answers[i]) {
			scores[1]++;
		}
		if (third[i % third.length] === answers[i]) {
			scores[2]++;
		}
	}

	const maxScore = Math.max(...scores);

	return scores.reduce((acc, cur, idx) => {
		if (cur === maxScore) {
			acc.push(idx + 1);
		}
		return acc;
	}, []);
}
```
