# 알고리즘 11주차

- 주제: 동적계획법
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/11/01 ~ 11/07

## 목차

- 동적계획법(Dynamic Programming)

  - 문제 1) https://leetcode.com/problems/maximum-subarray/
  - 문제 2)

# 동적계획법 1 - 53. Maximum Subarray

- 문제 분류: `분할정복법`
- 문제 출처: [Leetcode - 53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- 라벨: `Easy`, `JavaScript`

## 문제

## 풀이

- 절댓값이 더 큰 음수는 더해봤자이기 때문에 제외해야한다.

```js
const maxSubArray = (nums) => {
  let max = nums[0];
  let current = Math.max(max, 0);

  for (let i = 1; i < nums.length; i++) {
    current += nums[i];
    max = Math.max(max, current);
    current = Math.max(current, 0);
  }

  return max;
};
```

- 시간 복잡도: `O(n)`

![image](https://user-images.githubusercontent.com/33214449/140477827-a64c2e91-59aa-4796-b3e1-2b5f89fcf215.png)

## Ref

- [Leetcode Discussion - Kadane 방식 코드참고](https://leetcode.com/problems/maximum-subarray/discuss/562928/JavaScript-Kadane's-algorithm-implementation-w-explanation)

# 동적계획법 2 -

- 문제 분류: `분할정복법`
- 문제 출처: [Leetcode - 53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- 라벨: `Easy`, `JavaScript`
