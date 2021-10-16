# 알고리즘 9주차

- 주제: 비트 조작, 슬라이딩 윈도우
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/10/04 ~10/10

## 목차

- 비트 조작

  - 문제 1) https://leetcode.com/problems/single-number/
  - 문제 2) https://leetcode.com/problems/hamming-distance/

- 슬라이딩 윈도우
  - 문제 1) https://leetcode.com/problems/longest-repeating-character-replacement/
  - 문제 2) https://leetcode.com/problems/contains-duplicate-ii/

# 비트 조작 문제 1 - 136. Single Number

- 문제 분류: `비트조작`
- 문제 출처: [Leetcode - 136. Single Number](https://leetcode.com/problems/single-number/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/137595009-7f7a408a-ca1f-458c-ad08-15bbd483f2f6.png)

- 제약조건
  - 선형 시간 복잡도에 문제를 해결해야한다.
  - constant extra space만 사용해야한다.?

## 풀이

- 서로 같은 값을 XOR 연산 했을 때 0이 나오는 것을 이용하여 문제를 푼다. (XOR은 비교하는 두 비트가 서로 다르면 1을 같으면 0을 반환한다.)

```js
let singleNumber = function (nums) {
  // 주어진 nums 배열의 원소가 1개인 경우 그 원소를 반환한다.
  if (nums.length === 1) return nums[0];

  const obj = {};

  // nums 배열의 원소를 돌면서...
  for (const num of nums) {
    // 처음 보는 숫자라면 객체 obj에 저장한다. key, value값 모두 그 숫자값을 갖도록 저장한다.
    if (obj[num] === undefined) {
      obj[num] = num;
      continue;
    }
    // 이미 한번 나왔던 숫자라면, 객체에 저장되어있는 숫자와 지금 숫자를 XOR 연산한 다음 Boolean 값으로 변환해 객체 obj에 저장한다. (false가 저장될 것이다)
    obj[num] = Boolean(obj[num] ^ num);
  }

  // obj 중에서 값이 false가 아닌 것을 찾아 리턴한다.
  for (const property in obj) {
    if (obj[property] !== false) {
      return obj[property];
    }
  }
};
```

- 시간 복잡도: `O(n)`

![image](https://user-images.githubusercontent.com/33214449/137594983-bc270b54-11e7-4934-8d8a-7d2309cca28c.png)

# 비트 조작 문제 2 - 461. Hamming Distance

- 문제 분류: `비트조작`
- 문제 출처: [Leetcode - 461. Hamming Distance](https://leetcode.com/problems/hamming-distance/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/137595267-814c6649-47c5-4c1d-9b1a-4e18a4cb5392.png)

## 풀이

- x와 y를 XOR 연산하면, 서로 비트가 다른 자리에만 1이 반환됨을 이용

- ex) x = 1, y = 4 라고 할 때,
  - x = 1(이진수로 0001), y = 4(이진수로 0100)
  - x ^ y = 1 ^ 4 = 5(이진수로 0101)
  - 위 결과를 이진수 string으로 변환 -> '0101'
  - 위 문자열을 한 문자씩 돌며 문자가 '1'인 경우 count를 증가시킨다.
  - count를 최종 반환한다.

```js
let hammingDistance = function (x, y) {
  const xorNum = x ^ y;
  const binXorNum = xorNum.toString(2);

  let cnt = 0;

  for (const bit of binXorNum) {
    if (bit === '1') cnt++;
  }

  return cnt;
};
```

![image](https://user-images.githubusercontent.com/33214449/137595568-8b589798-eab8-4a3d-9550-2595bd821605.png)

- 시간복잡도: `O(n)`
  - x, y를 XOR 연산 -> 2진수로 바꾼 문자열 -> 이 문자열의 길이 n만큼 반복

## Ref

- [JavaScript 10진수를 2진수로](https://minhanpark.github.io/today-i-learned/binary-change/)

# 슬라이딩 윈도우 문제 1 - 424. Longest Repeating Character Replacement

- 문제 분류: `슬라이딩윈도우`
- 문제 출처: [Leetcode - 424. Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
- 라벨: `Medium`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/136651492-b68bf403-a028-4ccb-85c8-58b1dbf261eb.png)

## 풀이

- `start`: 윈도우의 시작 인덱스
- `end`: 윈도우의 끝 인덱스
- `max_len`: 결과값. 같은 문자만 포함되도록 k개를 바꿔서 만들 수 있는 서브스트링 중 가장 긴 길이.
- `maxCnt`: 윈도우 내에서 가장 많이 나타나는 문자의 개수
- `arr`: 윈도우 내에서 나타나는 문자의 개수를 담은 배열

| 문자       | A   | B   | C   | ... | X   | Y   | Z   |
| ---------- | --- | --- | --- | --- | --- | --- | --- |
| 인덱스     | 0   | 1   | 2   | ... | 23  | 24  | 25  |
| 값(초기값) | 0   | 0   | 0   | ... | 0   | 0   | 0   |

- for: 문자열의 길이만큼 반복한다. (`end`: 0 ~ 문자열의 길이-1)
  - `maxCnt` 값을 갱신한다.
  - if: `윈도우의 크기 - 윈도우 내에서 가장 많은 문자의 개수`가 `k`보다 크다면 `k`개를 바꾼다해도 같은 문자로 만들 수 없으므로 윈도우를 옮긴다.(윈도우의 시작인덱스를 한 칸 증가시키고 이때 제외된 문자의 count를 감소시킴)
  - else: 현재까지의 `max_len`를 구해 갱신한다.

```js
var characterReplacement = function (s, k) {
  let start = 0; // window start index
  let max_len = 0; // result variable

  const arr = new Array(26).fill(0);
  let maxCnt = 0;

  for (let end = 0; end < s.length; end++) {
    const char = s[end];
    maxCnt = Math.max(maxCnt, ++arr[char.charCodeAt() - 'A'.charCodeAt()]);

    if (end - start + 1 - maxCnt > k) {
      arr[s[start++].charCodeAt() - 'A'.charCodeAt()]--;
    } else {
      max_len = Math.max(max_len, end - start + 1);
    }
  }

  return max_len;
};
```

- 시간 복잡도: `O(n)`
  - n: 주어진 문자열 `s`의 길이

![image](https://user-images.githubusercontent.com/33214449/136651715-41bcafb4-e49b-4a0c-b945-73e9d36dd365.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/longest-repeating-character-replacement/discuss/181382/Java-Sliding-Window-with-Explanation)

# 슬라이딩 윈도우 문제 2 - 219. Contains Duplicate II

- 문제 분류: `슬라이딩윈도우`
- 문제 출처: [Leetcode - 219. Contains Duplicate II](https://leetcode.com/problems/contains-duplicate-ii/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/136665707-0db33dd2-af07-4bdc-ad23-c50c06d5c718.png)

## 풀이

- 슬라이딩 윈도우 박스의 양 끝 데이터를 이용해서 문제를 풀어야겠다고 까진 생각을 했으나 문제가 잘 풀리지 않았다. Leetcode Discuss에 여기에 Set을 활용하면 간단하게 풀 수 있길래 해당 코드를 참고했다.

- 슬라이딩 위도우의 시작을 `start`로, 끝을 `end`로 정해놓고 `end`값을 증가시키는 for문을 돌린다.
- 두 값이 같으면서 최대 `k`만큼 떨어져있는 경우가 있는지 알아내야한다.
  - `end - start`가 k보다 작거나 같으면 Set을 이용하여 같은 값인지 바로 검사한다.
  - `end - start`가 k를 넘어서면 `start`값을 조정해 슬라이딩윈도우 박스 크기를 줄인다. 또한 `start`에 있는 요소를 Set에서 제거한다.

```js
var containsNearbyDuplicate = function (nums, k) {
  let set = new Set();
  let start = 0;
  for (let end = 0; end < nums.length; end++) {
    if (end - start > k) {
      set.delete(nums[start]);
      start++;
    }
    if (set.has(nums[end])) return true;
    set.add(nums[end]);
  }

  return false;
};
```

- 시간 복잡도: `O(n)`
  - n: `nums`의 길이

![image](https://user-images.githubusercontent.com/33214449/136665689-36aa13f4-c3e0-4e1d-aa91-8713fa094a1c.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/contains-duplicate-ii/discuss/61619/Java-solution-using-Set-and-sliding-window) 첫번째 댓글
