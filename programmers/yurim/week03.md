# 알고리즘 3주차

- 주제: 정렬, 완전탐색
- 작성자: 박유림(Wol-dan) / @pul8219

## 목차

- 정렬
  - 문제 1) [K번째수](#k번째수)
  - 문제 2) [가장 큰 수](#가장-큰-수)
- 완전탐색
  - 문제 1) [모의고사](#모의고사)
  - 문제 2) [소수 찾기](#소수-찾기)

# K번째수

- 문제 분류: `정렬`
- 문제 출처: [프로그래머스 level01. K번째수](https://programmers.co.kr/learn/courses/30/lessons/42748)
- 라벨: `Level 1`, `JavaScript`

## 문제

commands 배열은 [i, j, k] 형태의 원소를 가지는 2차원 배열이다. 1차원 배열 array에 대해 commands의 모든 각각의 원소를 적용해야 한다.

1. array의 i번째부터 j번째까지 자른다.
2. `1번`에서 나온 배열을 정렬한다.
3. `2번`에서 나온 (정렬된) 배열에서 k번째 숫자를 찾는다.
4. 이렇게 commands를 돌며 `3번`에서 나온 숫자들을 배열에 담아 최종적으로 리턴한다.

## 풀이 과정

- commands 배열을 `forEach`로 순회하며 아래 과정을 반복한다.
- `slice()` 함수를 이용해 array를 자른다.
- 잘린 배열을 slicing 변수에 담고, `sort()`로 정렬한다.
- slicing 배열에서 k번째 수를 찾아 answer 배열에 넣는다. (slicing 배열은 반복마다 초기화해서 사용한다.)

> 🏷️ Syntax
>
> - `Array.prototype.sort()`
>   - 그냥 `sort()`는 배열의 요소들을 아스키 코드 순서대로 정렬한다.(`[100, 1, 4, 13,10]` 을 `[1, 10, 100, 13,4]` 으로 정렬한다. -> 원하는 결과X) `sort(function(a, b){ return a - b; });` 와 같이 작성해야 숫자를 오름차순으로 정렬할 수 있다.
>   - 참고: [자바스크립트 정렬 함수, sort()](https://dudmy.net/javascript/2015/11/16/javascript-sort/)
> - 구조 분해 할당(Destructuring Assignment)
>   - ex) `[a, b] = [10, 20];`
>   - 참고: [구조 분해 할당 - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## 제출 코드

- 시간 복잡도: O(n^2) 으로 예상
  - `commands 반복 x sort로 정렬`
  - 자바스크립트의 `sort()` 함수가 호출될 때 정렬 알고리즘을 사용하는지는 JS엔진에 따라 달라질 수 있다고 한다.

```js
function solution(array, commands) {
  var answer = [];
  let slicing = [];
  commands.forEach((command) => {
    slicing = array.slice(command[0] - 1, command[1]); // array의 i ~ j번째까지 잘라 새로운 배열에 저장

    slicing.sort((a, b) => a - b); // 정렬

    answer.push(slicing[command[2] - 1]);

    slicing = []; // slicing 배열 초기화
  });
  return answer;
}
```

## 다른 풀이

```js
function solution(array, commands) {
  return commands.map(
    ([i, j, k]) => array.slice(i - 1, j).sort((a, b) => a - b)[k - 1]
  );
}
```

# 가장 큰 수

- 문제 분류: `정렬`
- 문제 출처: [프로그래머스 level02. 가장 큰 수](https://programmers.co.kr/learn/courses/30/lessons/42746)
- 라벨: `Level 2`, `JavaScript`

## 문제

- 0 또는 양의 정수로 이루어진 `numbers` 배열에서 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내는 문제
- 입력: 0 또는 양의 정수로 이루어진 배열
- 출력: 이어붙여 만들 수 있는 가장 큰 수를 알아내 문자열로 리턴

## 풀이 과정

- `numbers.map((num) => num + '')`: numbers 배열의 각 숫자들을 문자열로 변환한다.
- `sort((a, b) => b + a - (a + b))`: 문자열로 변환된 숫자들을 조합하며 비교해 정렬한다. ('6', '10' => '106'-'610' => '610'이 더 크기 때문에 '6'이 배열의 앞쪽으로 갈 것이다.)
- `join('')`: 정렬이 완료된 후 배열의 요소들을 잇는다.
- `return answer[0] === '0' ? '0' : answer;`: 문자열이 0으로만 구성되어있을 경우 0을 리턴한다.(`"0000"`일 수도 있기 때문)

> 🏷️ Syntax
>
> - `sort()`: `sort()`에는 매개변수로 함수가 들어갈 수 있다. 이 함수의 반환 값에 따라 비교되는 두 요소인 a, b의 순서가 정해진다.
>   - 음수: a, b(a를 b보다 낮은 인덱스로 정렬한다. = a가 먼저 온다.)
>   - 0: 그대로(a, b의 자리를 바꾸지 않음)
>   - 양수: b, a
> - 빈 배열에 map을 돌리면 당연히 돌지 않고 빈배열이 반환된다.
> - push() 할 때 인자가 생략되면 아무 것도 추가되지 않는다.(당연)

## 제출 코드

- 시간 복잡도: O(n^2)

  - `map`은 n번 돈다. (❓ map과 sort를 중첩으로 인식해야하는지?)
  - `sort()`에서 비교할 때 비교하는 횟수가 n, n-1, n-2, ... 이렇게 작아질 것 같기 때문

```js
function solution(numbers) {
  let answer = '';

  answer = numbers
    .map((num) => num + '')
    .sort((a, b) => b + a - (a + b))
    .join('');
  return answer[0] === '0' ? '0' : answer;
}
```

## 다른 풀이(통과X)

- 순열을 이용해 모든 경우의 수를 구한 뒤 이중에서 최대값을 구했다.
- 테스트 케이스 2가지는 통과하나 제출시 `signal: aborted (core dumped)`나 `런타임 에러`가 발생한다. 리턴조건이 잘못 작성되어 재귀 호출이 너무 깊어져 에러가 나는건가 싶은데 정확히 모르겠다.

```js
function getPermutations(arr) {
  const selectNumber = arr.length;
  arr = arr.map((n) => n + ''); // arr의 모든 요소를 문자열로 변환

  const results = [];
  if (selectNumber === 1) return arr.map((value) => [value]); // 1개씩 택할 때, 바로 모든 배열의 원소 return

  arr.forEach((fixed, index, origin) => {
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)]; // 해당하는 fixed를 제외한 나머지 배열
    const permutations = getPermutations(rest, selectNumber - 1); // 나머지에 대해 순열을 구한다.
    const attached = permutations.map((permutation) => [fixed, ...permutation]); // 돌아온 순열에 대해 떼 놓은(fixed) 값 붙이기
    results.push(...attached); // 배열 spread syntax 로 모두다 push
  });
  return results; // 결과 담긴 results return
}

function solution(numbers) {
  let answer = 0;
  let results = [];
  results = getPermutations(numbers).map((v) => Number(v.join('')));
  answer = Math.max(...results) + '';

  return answer;
}

const numbers = [3, 30, 34, 5, 9];
const result = solution(numbers);
```

## References

- [JavaScript로 순열과 조합 알고리즘 구현하기](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-%EC%88%9C%EC%97%B4%EA%B3%BC-%EC%A1%B0%ED%95%A9-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-21df4b536349)

- [Array.prototype.sort() - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

- [JS 프로그래머스 - 가장 큰 수(레벨2)](https://taesung1993.tistory.com/20) 코드 참고

# 모의고사

- 문제 분류: `완전탐색`
- 문제 출처: [프로그래머스 level01. 모의고사](https://programmers.co.kr/learn/courses/30/lessons/42746)
- 라벨: `Level 1`, `JavaScript`

## 문제

- 입력: 모의고사 정답이 순서대로 담긴 배열 `answers`
- 출력: 정답을 가장 많이 맞춘 사람의 번호를 배열에 담아 리턴(오름차순으로 정렬할 것)

- 1번 수포자가 정답을 찍는 방식: 1, 2, 3, 4, 5, ...(반복)
- 2번 수포자가 정답을 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, ...(반복)
- 3번 수포자가 정답을 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...(반복)

## 풀이 과정

- 문제수에 맞춰 1,2,3번 수포자의 정답지를 담은 배열 확장(`extendArr()함수`)
- `answers`의 length만큼 돌며 1,2,3번 수포자의 정답지와 비교해 사람마다 정답을 맞춘 개수를 리턴(`compArr()함수`)
- 가장 많이 맞춘 정답 개수를 찾아 `max` 변수에 저장. `max`만큼 정답을 맞춘 사람을 찾아 `answer` 배열에 저장(가장 많이 맞힌 사람이 여러명일 수 있음)
- `answer` 배열을 오름차순으로 정렬하고 최종적으로 리턴

## 제출 코드

- 시간 복잡도: O(n)

```js
function extendArr(arr, len) {
  const div = len / arr.length;
  let result = [];
  if (div <= 1) {
    return arr;
  } else {
    if (len % arr.length === 0) {
      for (let i = 0; i < Math.floor(div); i++) {
        result = [...result, ...arr];
      }
    } else {
      for (let i = 0; i < Math.floor(div) + 1; i++) {
        result = [...result, ...arr];
      }
    }
    return result;
  }
}

function compArr(arr, answers) {
  // 맞춘 개수를 리턴
  let count = 0;
  for (let i = 0; i < answers.length; i++) {
    if (arr[i] === answers[i]) count++;
  }
  return count;
}

function solution(answers) {
  var answer = [];
  const obj = [];

  const one = [1, 2, 3, 4, 5];
  const two = [2, 1, 2, 3, 2, 4, 2, 5];
  const three = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

  const new_one = extendArr(one, answers.length);
  const new_two = extendArr(two, answers.length);
  const new_three = extendArr(three, answers.length);

  obj.push({
    id: 1,
    ans_cnt: compArr(new_one, answers),
  });
  obj.push({
    id: 2,
    ans_cnt: compArr(new_two, answers),
  });
  obj.push({
    id: 3,
    ans_cnt: compArr(new_three, answers),
  });

  const max = obj.reduce((a, b) => (a.ans_cnt > b.ans_cnt ? a : b)).ans_cnt;
  const new_obj = obj.filter((elem) => elem.ans_cnt === max);
  answer = new_obj.map((elem) => elem.id);
  answer.sort((a, b) => a - b);

  return answer;
}
```

# 소수 찾기

- 문제 분류: `완전탐색`
- 문제 출처: [프로그래머스 level02. 소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/42839)
- 라벨: `Level 2`, `JavaScript`

## 문제

- 입력: 문자열(`"013"`은 0, 1, 3 숫자가 적힌 종이 조각이라는 의미)
- 출력: 종이 조각에 쓰여진 숫자를 조합해 만들 수 있는 **소수**가 몇개인지 리턴 = 숫자

## 풀이 과정

- 시간 복잡도: O(n^3) 예상

  - `solution()` 내부 for문(numbers의 길이가 n이라고 가정할 때 n번 반복)
  - `getPermutations()` 내부 forEach문(최대 n번 반복)
  - `solution()`의 `map`

- numbers 문자열을 `split()`으로 쪼개 배열(`splitArr`)로 만든다.
- `getPermutations()` 함수를 사용해 조합가능한 모든 경우를 구한다. (`numbers`의 숫자가 `"011"`이라면 이중에서 1개, 2개, 3개를 뽑아 조합가능한 모든 경우를 구한다.)
- 조합가능한 경우(ex.`["0", "1"]`)를 `join()`으로 이어붙이고(`"01"`) 숫자로 바꾼다.(`1`이됨) 이를 배열(`candiArr`)에 추가한다.
- 조합가능한 경우가 담긴 배열(`candiArr`)을 Set(`candiSet`)으로 만들어 중복을 제거한다.
- Set(`candiSet`)에서 하나씩 꺼내며 소수인지 검사하고 소수인 경우 `answer`를 증가시킨다.

## 제출 코드

```js
function getPermutations(arr, selectNumber) {
  const results = [];
  if (selectNumber === 1) return arr.map((v) => [v]);
  else {
    arr.forEach((fixed, index, origin) => {
      const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
      const permutations = getPermutations(rest, selectNumber - 1);
      const attached = permutations.map((permutation) => [
        fixed,
        ...permutation,
      ]);
      results.push(...attached);
    });
  }

  return results;
}

// 소수인지 판별
function isPrime(num) {
  // 소수는 1과 자기 자신만으로만 나누어 떨어지는 수 임으로
  // num > i
  for (let i = 2; num > i; i++) {
    if (num % i === 0) {
      //이 부분에서 num이  다른 수로 나눠떨어진다면 소수가 아님
      return false;
    }
  }
  // 소수는 1보다 큰 정수임으로
  // 1보다 작으면 false를 리턴한다
  return num > 1;
}

function solution(numbers) {
  let answer = 0;

  const candiArr = [];

  const splitArr = numbers.split('');
  for (let i = 1; i < numbers.length + 1; i++) {
    candiArr.push(
      ...getPermutations(splitArr, i).map((v) => Number(v.join('')))
    );
  }

  const candiSet = new Set(candiArr);
  candiSet.forEach(function (v) {
    if (isPrime(v)) answer++;
  });

  return answer;
}
```

![image](https://user-images.githubusercontent.com/33214449/130092530-b3ae0447-c2da-4476-90ff-dfc91f59b670.png)

- 실행 시간이 오래 걸리는 것 같아서 개선하고 싶다.

## References

- [JavaScript로 순열과 조합 알고리즘 구현하기](https://jun-choi-4928.medium.com/javascript%EB%A1%9C-%EC%88%9C%EC%97%B4%EA%B3%BC-%EC%A1%B0%ED%95%A9-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-21df4b536349) 순열 코드 출처

- [소수(Prime number) 판별법 [ JavaScript ]](https://velog.io/@loocia1910/javascript%EC%97%90%EC%84%9C-%EC%86%8C%EC%88%98Prime-number-%EA%B5%AC%ED%95%98%EA%B8%B0) 소수 판별 코드 출처
