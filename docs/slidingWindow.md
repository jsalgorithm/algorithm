# 슬라이딩 윈도우(Sliding Window)

고정된 크기의 윈도우(사각 박스라고 생각하기)를 이동시키면서 그 윈도우 안에 있는 데이터를 이용해 문제를 푸는 알고리즘을 의미한다.

# 문제를 풀며 알아보는 슬라이딩 윈도우

![image](https://user-images.githubusercontent.com/33214449/136386478-fcb63fa6-5142-465e-a7aa-28d4eb8b97dd.png)

예를 들어 정수로 이루어진 배열이 주어지고, 길이가 k인 서브배열의 합계 중 가장 큰 합계를 구하는 문제가 있다고 해보자.

(서브배열은 연속적으로 이루어진 부분배열을 의미한다.)

먼저 이중 for문을 이용하여 문제를 풀면 아래와 같다. 입력으로 받은 배열을 돌면서 특정 길이(`k`)개 요소들의 합계를 구해서 최댓값을 구하는 방법이다.

```js
let maxSumOfSubarray = function (arr, k) {
  let maxSum = Number.MIN_VALUE;
  const arrSize = arr.length;

  for (let i = 0; i < arrSize - k + 1; i++) {
    let curSum = 0;
    for (let j = i; j < i + k; j++) {
      curSum += arr[j];
    }
    maxSum = Math.max(maxSum, curSum);
  }

  return maxSum;
};

console.log(maxSumOfSubarray([2, 4, 7, 10, 8, 4], 3));
```

위 코드를 좀 더 효율적으로 바꿀 수 있지 않을까?

잘보면 `2, 4, 7`을 더할 때와 `4, 7, 10`을 더할 때, `4, 7`이라는 요소가 중복된다. 위 방법은 순회마다 매번 서브배열의 합계를 계산한다. (4, 7을 다시 더한다는 것) 슬라이딩 윈도우를 이용하면 순회마다 서브배열의 합계를 매번 계산하는 반복적인 과정을 거치지 않고도 문제를 해결할 수 있다. 윈도우의 처음과 끝만 잘 조절하면 된다. 코드로 이해해보자.

- `window_start`: 슬라이딩 윈도우의 시작 인덱스
- `window_end`: 슬라이딩 윈도우의 끝 인덱스
- `window_sum`: 슬라이딩 윈도우 안에 있는 요소들의 합계

```js
let maxSumOfSubarray = function (arr, k) {
  let max_sum = Number.MIN_VALUE;
  const arrSize = arr.length;
  let window_sum = 0;
  let window_start = 0;

  for (let window_end = 0; window_end < arrSize; window_end++) {
    window_sum += arr[window_end];

    if (window_end >= k - 1) {
      max_sum = Math.max(max_sum, window_sum);
      window_sum -= arr[window_start];
      window_start++;
    }
  }

  return max_sum;
};

console.log(maxSumOfSubarray([2, 4, 7, 10, 8, 4], 3));
```

슬라이딩 윈도우 시작에 있는 요소를 빼주고, 끝에 있는 요소를 더해주며 코드가 진행된다. 사이에 중복된 요소들은 처음부터 다시 더하는게 아니라 이전에 더했던 값을 재사용한다.

슬라이딩 윈도우의 범위가 `k`보다 커질 때까지는 요소들을 합산하기만 하다가 `k`가 되면 슬라이딩 윈도우를 이동시키며 값을 계산한다.

아래 테이블은 반복문이 진행되는 과정을 나타낸 것이다.

| 반복          | 대괄호는 슬라이딩윈도우를 의미 | 변수값 변화                                                                                                         |
| ------------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| 첫번째반복    | [2] , 4, 7, 10, 8, 4           | window_sum = 2 <br /> window_start = 0 <br/> window_end = 0 <br/> max_sum = 0                                       |
| 두번째반복    | [2, 4], 7, 10, 8, 4            | window_sum = 6 [2+4] <br /> window_start = 0 <br/> window_end = 1 <br/> max_sum = 0                                 |
| 세번째반복    | [2, 4, 7], 10, 8, 4            | window_sum = 13 [2+4+7] <br /> window_start = 0 <br/> window_end = 2 <br/> max_sum = 13 [max(Number.MIN_VALUE, 13)] |
| 네번째 반복   | 2, [4, 7, 10], 8, 4            | window_sum = 21 [13+10-2] <br /> window_start = 1 <br/> window_end = 3 <br/> max_sum = 21[max(13, 21)]              |
| 다섯번째 반복 | 2, 4, [7, 10, 8], 4            | window_sum = 25 [21+8-4] <br /> window_start = 2 <br/> window_end = 4 <br/> max_sum = 25 [max(21, 25)]              |
| 여섯번째 반복 | 2, 4, 7, [10, 8, 4]            | window_sum = 22 [25+4-7] <br /> window_start = 3 <br/> window_end = 5 <br/> max_sum = 25 [max(25, 22)]              |

이렇게 슬라이딩 윈도우를 이용하면 중첩 for문을 사용하지 않고도 (단일 for문으로) 문제를 해결할 수 있다. 매번 처리되는 중복 요소를 버리지 않고 재사용함으로써 연산수가 적어지기 때문에 효율적이다.

# 예제

https://leetcode.com/problems/longest-substring-without-repeating-characters/

중복되는 문자가 없는 가장 긴 서브스트링 길이를 구하는 문제이다.

주어진 문자열이 `'pwwkew'`일 때 `'pwke'`와 같이 떨어진 문자열은 경우의 수에 포함되지 않으며 서브스트링이 아니다. 서브스트링은 요소가 연속되어야한다.

```
변수의 의미

w_start: 윈도우 시작 인덱스
w_end: 윈도우 끝 인덱스
max_len: 가장 긴 서브스트링 길이를 담을 변수
used: 이미 포함된 문자인지 알 수 있는 정보를 담은 객체. (문자: 인덱스) 형태로 저장한다.
```

- for: 문자열을 순회한다. 문자와 그 문자의 인덱스(w_end로 사용)를 인자로 받아 순회 때 사용한다.
  - if: 해당 문자가 `used`객체 안에 있고, 윈도우 시작 인덱스(`w_start`)가 이미 있는 그 문자의 인덱스보다 작거나 같으면 (이 조건이 있는 이유는 이미 윈도우 범위 밖의 문자라면 신경쓰지 않아도 되기 때문이다.)
    - 윈도우 시작 인덱스(`w_start`)값을 변경한다. 이미 중복된 문자 그 다음 인덱스를 가리키도록!
  - else: (윈도우안에서 처음 보는 문자라면)
    - 서브스트링 길이의 최댓값을 찾아 `max_len`변수를 갱신한다.
  - 현재 문자와 인덱스 정보를 used 객체에 추가. `used[char] = w_end;`

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  let w_start = 0;
  let max_len = 0;
  const used = {};

  [...s].forEach((char, w_end) => {
    console.log(used[char]);
    // used.hasOwnProperty(char) 이렇게 안 쓰고 used[char] 이렇게 쓰면 used[char]가 0인 경우도 false가 되서 정상적으로 동작하지 않음.
    if (used.hasOwnProperty(char) && w_start <= used[char]) {
      w_start = used[char] + 1;
    } else {
      max_len = Math.max(max_len, w_end - w_start + 1);
    }
    used[char] = w_end;
  });
  return max_len;
};
```

- forEach로 반복을 돌리기 위해 문자열 `s`를 전개연산자를 이용해 배열로 만들어주었다.

ex) `s = "abcabcbb"`인 경우 반복문이 진행되는 과정을 보면 다음과 같다.

```
for1
char = "a"
w_start = 0
w_end = 0
max_len = 1 [max(0, 1)]
used = { a: 0 }

for2
char = "b"
w_start = 0
w_end = 1
max_len = 2 [max(1, 2)]
used = { a: 0, b: 1 }

for3
char = "c"
w_start = 0
w_end = 2
max_len = 3 [max(2, 3)]
used = { a: 0, b: 1, c: 2 }

for4
char = "a"
w_start = 1 [0 + 1]
w_end = 3
max_len = 3 (갱신x)
used = { a: 3, b: 1, c: 2 }
지금 상태: a, [ b, c, a,] b, c, b, b

for5
char = "b"
w_start = 2 [1 + 1]
w_end = 4
max_len = 3 (갱신x)
used = { a: 3, b: 4, c: 2 }
지금 상태: a, b, [ c, a , b,] c, b, b

for6
char = "c"
w_start = 3 [2 + 1]
w_end = 5
max_len = 3 (갱신x)
used = { a: 3, b: 4, c: 5 }
지금 상태: a, b, c, [ a , b, c,] b, b

for7
char = "b"
w_start = 5 [4 + 1]
w_end = 6
max_len = 3 (갱신x)
used = { a: 3, b: 6, c: 5 }
지금 상태: a, b, c, a , b, [ c, b,] b

for8
char = "b"
w_start = 7[6 + 1]
w_end = 7
max_len = 3(갱신x)
used = { a: 3, b: 7, c: 5 }
지금 상태: a, b, c, a , b, c, b, [b]
```

# Ref

- [[알고리즘] 슬라이딩 윈도우 알고리즘](https://blog.fakecoding.com/archives/algorithm-slidingwindow/)
- [슬라이딩 윈도우(Sliding Window)](https://velog.io/@zwon/%EC%8A%AC%EB%9D%BC%EC%9D%B4%EB%94%A9-%EC%9C%88%EB%8F%84%EC%9A%B0Sliding-Window)
- [(C++) 투포인터 알고리즘, 슬라이딩 윈도우 알고리즘, Prefix Sum 구간합](https://ansohxxn.github.io/algorithm/twopointer/)
- [javascript에서 object안에 특정 key가 존재하는지 확인하는 방법](https://negabaro.github.io/archive/js-exists_keys_in_object)
