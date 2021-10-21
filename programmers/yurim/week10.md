# 알고리즘 10주차

- 주제: 분할정복법, 그리디알고리즘
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/10/18 ~ 10/24

## 목차

- 분할정복법

  - 문제 1) https://leetcode.com/problems/contains-duplicate/submissions/
  - 문제 2) 

- 그리디알고리즘
  - 문제 1) 
  - 문제 2) 

# 분할정복법 1 - 217. Contains Duplicate

- 문제 분류: `분할정복법`
- 문제 출처: [Leetcode - 217. Contains Duplicate](https://leetcode.com/problems/contains-duplicate/submissions/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/138316509-bc23f4e0-4b7f-469e-b84e-55f4959755c4.png)


## 풀이

```js
const containsDuplicate = function(nums) {
    return nums.sort((a,b) => a-b).some((num, index, arr) => num === arr[index-1]);
};

gdgd
```

분할정복법 중 병합 정렬같은 개념을 이용하여 풀이할 수 있는지 궁금하다.(배열을 반씩 쪼개가며 검사한다던가)

- 시간 복잡도: `O(n log n)`
    - `sort()`의 경우 JS엔진마다 다르긴 하지만 보통 `O(n log n)`의 시간 복잡도를 가진다고 한다.

![image](https://user-images.githubusercontent.com/33214449/138316375-fd1981da-5dee-4acb-b957-a5385b6cb7a7.png)
