# 정렬(Sort)

## k번째 수

```
function solution(array, commands) {
	const answer = [];
	for (let a = 0; a < commands.length; a++) {
		let i = commands[a][0];
		let j = commands[a][1];
		let k = commands[a][2];

		let copyArray = array.slice(i - 1, j);
		copyArray.sort((a, b) => a - b);
		answer.push(copyArray[k - 1]);
	}
	console.log(answer);
	return answer;
}

solution(
	[1, 5, 2, 6, 3, 7, 4],
	[
		[2, 5, 3],
		[4, 4, 1],
		[1, 7, 3],
	]
);

/* 
sort의 경우, 원본이 변경되는 정렬.
유니코드로 정렬하기 때문에 따로 compare 함수의 형식을 취해줘야 함.
sort method는 배열의 종류에 따라 다른 알고리즘을 사용한다.
숫자배열은 퀵정렬을 사용하고
숫자가 아닌 배열은 병합정렬을 사용한다.
그러나 sort()가 항상 최선의 알고리즘이 아닐 수 있기 때문에 정렬 알고리즘을 알아야한다..
slice의 경우, 복사본 배열을 반환하기 때문에 변수에 넣어주었다.
*/
```

1. 풀이내용
   1. 주어진 commands의 길이만큼 반복문을 시행한다.
   2. I,j,k를 각각의 반복문 내에서 설정해준다.
   3. 배열을 slice 메서드를 이용해i -1번째의 요소부터 j까지의 요소까지 자른다.
   4.  해당 배열을 sort한 후 k-1번째 인덱스에 있는 값을 answer에 push한다.
2. 시간복잡도

- 반복문을 이용하기 때문에, O(n)
- 숫자배열의 경우 퀵정렬을 사용함. 퀵정렬은 O(nlogn)만큼의 시간복잡도를 가진다.



## 가장 큰 수

```
function solution(numbers) {
	let temp = numbers.map((a) => String(a)).sort((a, b) => b + a - (a + b));

	return temp.join("");
}
console.log(solution([6, 10, 2]));

/**
 * 숫자들을 String으로 변환
 * 이어지는 숫자의 크기를 비교했을 때
 * b+a < a+b (ex : 30+3 < 3+30)이면 두 숫자의 위치를 변경한다.
 * join 메서드를 이용해 배열의 모든 요소를 연결해 문자열로 만듦
 */

```

1. 풀이과정
   1. 주석 참고
2. 시간복잡도
   1. map함수는 O(n)의 시간복잡도를 가진다. 
      1. 콜백함수의 결과값으로 새로운 배열을 반환하고, 각 원소마다 실행된다는 점에서 forEach와 같다.
   2. sort 메서드는 O(nlogn)의 시간복잡도를 가진다.

## 모의고사

```
function solution(answers) {
	const answer = [];
	const supoja1 = [1, 2, 3, 4, 5];
	const supoja2 = [2, 1, 2, 3, 2, 4, 2, 5];
	const supoja3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];
	let count1 = 0;
	let count2 = 0;
	let count3 = 0;
	for (let i = 0; i < answers.length; i++) {
		if (supoja1[i % supoja1.length] === answers[i]) count1++;
		if (supoja2[i % supoja2.length] === answers[i]) count2++;
		if (supoja3[i % supoja3.length] === answers[i]) count3++;
	}
	console.log(count1, count2, count3);
	if (count1 >= count2 && count1 >= count3) answer.push(1);
	if (count2 >= count1 && count2 >= count3) answer.push(2);
	if (count3 >= count1 && count3 >= count2) answer.push(3);
	console.log(answer);
	return answer;
}

solution([1, 3, 1, 1, 2, 4, 2, 5]);
```

1. 풀이내용
   1. 주어진 수포자들의 답안을 배열로 정리
   2. 반복문을 이용해 정답의 개수를 카운트
   3. 단, **정답의 길이 > 수포자가 쓴 답의 길이**일 경우가 발생하므로, 인덱스를 나머지값으로한다.
   4. 비교연산을 통해 가장 크거나 같은수를 answer에 push

## 소수찾기

```
const permutation = (arr, selectNum) => {
	let result = [];
	if (selectNum === 1) return arr.map((value) => [value]);

	arr.forEach((fixed, index, origin) => {
		const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
		const permutations = permutation(rest, selectNum - 1);
		const attached = permutations.map((permutations) => [
			fixed,
			...permutations,
		]);
		result.push(...attached);
	});
	return result;
};

const isPrime = (num) => {
	if (num === 1 || num === 0) return false;
	if (num === 2) return true;
	for (let i = 2; i < num / 2 + 1; i++) {
		if (num % i === 0) return false;
	}
	return true;
};

function solution(numbers) {
	let answer = 0;
	const arr = numbers.split("");
	const set = new Set();

	for (let i = 1; i <= numbers.length; i++) {
		const result = permutation(arr, i).map((res) => +res.join(""));
		result.forEach((res) => {
			if (!set.has(res)) {
				set.add(res);
				answer += isPrime(res) ? 1 : 0;
			}
		});
	}

	return answer;
}

solution("17");
```

1. 풀이내용
   1. 완전탐색에서 자주 나오는 순열을 이용해야하는 문제였던 것 같다..
   2. 하..너무 피곤해..내일..마저 쓰겠읍니다.





## ref

https://kimyejin.tistory.com/m/62