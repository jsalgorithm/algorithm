# 알고리즘 2주차

- 주제: 이분탐색, 해시
- 작성자: 박유림(Wol-dan) / @pul8219

## 목차

- 이분 탐색(이진 탐색)
  - 문제 1) [Intersection of Two Arrays II](#intersection-of-two-arrays-ii)
  - 문제 2) [Find the Duplicate Number](#find-the-duplicate-number)
- 해시
  - 문제 1) [완주하지 못한 선수](#완주하지-못한-선수)
  - 문제 2) [위장](#위장)

# Intersection of Two Arrays II

- 문제 분류: `이분 탐색(이진 탐색)`
- 문제 출처: [LeetCode - 350. Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)
- 라벨: `Easy`, `JavaScript`

## 문제

## 풀이 과정

## 제출 코드

## References

# Find the Duplicate Number

- 문제 분류: `이분 탐색(이진 탐색)`
- 문제 출처: [LeetCode - 287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)
- 라벨: `Medium`, `JavaScript`

## 문제

## 풀이 과정

## 제출 코드

## References

# 완주하지 못한 선수

- 문제 분류: `해시`
- 문제 출처: [프로그래머스 Level 1 - 완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)
- 라벨: `Level 1`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/130213203-fa9770b1-060b-4721-b0eb-596bcaa44924.png)

- 입력: 마라톤에 참가자 이름이 든 배열(`participant` 배열), 그중 마라톤 완주에 성공한 완주자들의 이름이 든 배열(`completion` 배열)
- 출력: 완주하지 못한 선수의 이름(`String`)

- 완주하지 못한 선수는 1명이다.
- 참가 선수 중엔 동명이인이 있을 수 있다.

## 풀이 과정

- 처음에 했던 생각: `participant` 배열을 돌면서 `completion`에 있는 이름이면 `participant`에서 제거한다. 반복을 마치면 `participant`에 완주하지 못한 1개의 이름이 남을 것이고 이를 리턴한다.(but 인자로 들어온 배열을 변경한다는 단점이 있다.) -> 하지만 이 방법이 아니라 해시 개념을 이용해서 풀고 싶었다. 해시는 키값으로 value를 찾는 방식. 해시 함수는 구현하지 못했다. 자료를 검색할 때 O(1)의 시간으로 해결할 수 있도록 해보자.

- 1. 참가자 명단(`participant`)을 순회하며 `key: 선수 이름, value: +1`로 Map에 key, value 쌍을 입력한다.
  - Map에 존재하지 않을 경우 `key: 선수 이름, value: 1`로 세팅한다.
  - Map에 이미 존재할 경우(동명이인이라는 뜻) 해당 key의 value를 1만큼 증가시킨다.
- 2. 완주자 명단(`completion`)을 순회하며 완주자 이름이 Map에 있으면 value를 1만큼 감소시킨다.
- 1,2번이 끝나면 Map을 `for...of`로 순회하면서 value가 1 이상이면 해당 선수의 이름을 answer 변수에 넣는다. 그리고 break로 반복을 빠져나간다. (완주한 경우: value는 0 / 완주하지 못한 경우: value는 1 이상일 것)

## 제출 코드

- 시간 복잡도: O(n)

```js
function solution(participant, completion) {
  let answer = '';
  let hashMap = new Map();

  participant.map((el) => {
    if (!hashMap.get(el)) hashMap.set(el, 1);
    else hashMap.set(el, hashMap.get(el) + 1);
  });

  completion.map((el) => {
    hashMap.set(el, hashMap.get(el) - 1);
  });

  for (const [key, value] of hashMap) {
    if (value >= 1) {
      answer = key;
      break;
    }
  }

  return answer;
}
```

## References

- 코드 참고: [[프로그래머스 JavaScript] 완주하지 못한 선수 - Map 사용](https://ghost4551.tistory.com/53)

# 위장

- 문제 분류: `해시`
- 문제 출처: [프로그래머스 Level 2 - 위장](https://programmers.co.kr/learn/courses/30/lessons/42578)
- 라벨: `Level 2`, `JavaScript`

## 문제

## 풀이 과정

## 제출 코드

## References
