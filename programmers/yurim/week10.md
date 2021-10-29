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
const containsDuplicate = function (nums) {
  return nums
    .sort((a, b) => a - b)
    .some((num, index, arr) => num === arr[index - 1]);
};
```

분할정복법 중 병합 정렬같은 개념을 이용하여 풀이할 수 있는지 궁금하다.(배열을 반씩 쪼개가며 검사한다던가)

- 시간 복잡도: `O(n log n)`
  - `sort()`의 경우 JS엔진마다 다르긴 하지만 보통 `O(n log n)`의 시간 복잡도를 가진다고 한다.

![image](https://user-images.githubusercontent.com/33214449/138316375-fd1981da-5dee-4acb-b957-a5385b6cb7a7.png)

# 분할정복법 2 - 121. Best Time to Buy and Sell Stock

- 문제 분류: `분할정복법`
- 문제 출처: [Leetcode - 121. Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/138424739-5c21934b-4c8f-4b9c-a0d4-1634b578a6d9.png)

## 풀이1 (통과X)

- 테스트케이스 1개는 통과하나, Time Limit Exceeded로 코드 제출은 통과X
- 분할정복 아이디어로 풀 수 있는지 생각하려고 했으나 적용하진 못했음. 분할정복으로 풀 수 있는 아이디어 이해 필요!

- 반복
  - 가장 min 값 찾기
  - prices를 copy해놓은 배열에서 min값 뒤의 요소들만 판별 -> 그중 가장 큰 값 찾아서(대신 앞에서 구한 min보다 커야함) max profit 계산
  - 위에서 구했던 min값 배열에서 삭제

```js
const maxProfit = function (prices) {
  const copy_prices = prices.slice();
  const initMaxVal = Math.max(...copy_prices);
  let result = 0;
  let cnt = 0;

  // 종료 조건?
  while (!cnt) {
    const minVal = Math.min(...copy_prices);
    const minVal_idx = copy_prices.findIndex((elem) => elem === minVal);
    const targetArr = copy_prices.slice(minVal_idx + 1);
    const maxVal = Math.max(...targetArr);
    if (minVal < maxVal && maxVal - minVal > result) {
      result = maxVal - minVal;
      cnt = 1;
    }
    copy_prices.splice(minVal_idx, 1);
  }

  return result;
};
```

## 풀이2

- profit을 최대로 낼 수 있는 경우의 인덱스가 `i`, `j`라면
  - `i < j`
  - `prices[j] - prices[i]`가 최대
  - 여야 한다.

```js
const maxProfit = function (prices) {
  let profit = 0;
  let min = prices[0];

  for (let i = 1; i < prices.length; i++) {
    if (min > prices[i]) min = prices[i];
    else if (prices[i] - min > profit) profit = prices[i] - min;
  }

  return profit;
};
```

- 시간 복잡도: `O(n)`

![image](https://user-images.githubusercontent.com/33214449/138434369-70823a0a-9d89-4a01-9210-6d06c3ef547d.png)

## Ref

- [Leetcod Discussion](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/39267/Javascript-solution-if-anyone-is-interested) 댓글에 있는 코드 참고
- [Leetcode Discussion 분할정복법 풀이 예시](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/discuss/763051/5-methods-from-brute-force-to-most-optimised)

# 그리디알고리즘 1 - 455. Assign Cookies

- 문제 분류: `그리디알고리즘`
- 문제 출처: [Leetcode - 455. Assign Cookies]()
- 라벨: `Easy`, `JavaScript`

## 문제

- 입력:
  - `g[i]`: 아이 `i`가 받았을 때 만족하는 쿠키의 최소 사이즈
  - `s[j]`: 쿠키 `j`의 사이즈. (`s`의 총 길이 = 쿠키의 총 개수)
- 출력: 쿠키를 아이들에게 준다고 했을 때, 가장 많이 만족시킬 수 있는 아이들의 수

## 풀이

- `s`배열에서 가장 작은 사이즈의 쿠키부터 확인하면 최적의 경우를 구할 수 있어서 아래와 같이 문제를 풀이했다.

ex) `g = [1,2,4], s = [1,3,6]`인 경우

- 사이즈가 `6`인 쿠키로도 모든 아이들을 만족시킬 수 있지만, 만약 6크기의 쿠키로 아이 `g[0]`을, 3크기의 쿠키로 `g[1]`을, ... 이런 순서로 문제를 풀면 1크기의 쿠키로는 적어도 4크기의 쿠키를 원하는 `g[2]`를 만족시킬 수 없다. 즉 최적의 해가 구해지지 않는 것이다. 따라서 사이즈가 가장 작은 쿠키부터 배열 `g`에서 찾으면 최적의 해를 구할 수 있다.

- 입력값으로 들어온 g, s를 변경하지 않고 싶어서 copyG, copyS를 선언하여 g, s의 복사본을 만들어 사용했다.(얕은 복사)
- 매 반복마다 무조건 copyS의 0번째 요소를 삭제하는 이유: 이 사이즈의 쿠키로 만족시킬 수 있는 아이가 없는 경우에도 copyS에서 삭제해주어야하기 때문이다.

```js
const findContentChildren = function (g, s) {
  const copyG = g.slice();
  const copyS = s.slice().sort((a, b) => a - b);
  let result = 0;

  while (copyS.length !== 0) {
    copyG.some((elem, index) => {
      // copyS의 0번째 요소보다 같거나 작은 값이 copyG에 있으면
      if (elem <= copyS[0]) {
        result++; // result 값을 증가시킨다
        copyG.splice(index, 1); // copyG에서 찾은 그 값을 배열에서 삭제
        return true;
      }
      return false;
    });

    // copyS의 0번째 요소를 삭제
    copyS.splice(0, 1);
  }

  return result;
};
```

- 시간 복잡도: `O(n^2)`
  - sort log(n log n)
  - s의 길이만큼 반복(n이라고 가정)
    - g의 길이만큼 반복(n이라고 가정) -> 그래도 `Array.prototype.some()`을 사용했기 때문에 조건에 맞는 요소가 있으면 반복을 중단하고 바로 리턴할 것이다.

![image](https://user-images.githubusercontent.com/33214449/138412864-6388e370-f437-4220-9ed2-9048b306ed6e.png)

# 그리디알고리즘 2 -

- 문제 분류: `그리디알고리즘`
- 문제 출처: [Leetcode - ]()
- 라벨: `Easy`, `JavaScript`

## 문제

- 매일 주식을 사고팔 수 있다.
- 그러나 1주만 가지고 있을 수 있다.
- 산 날 당일에 파는 것도 가능하다.

## 풀이

이익이 최대가 될 수 있게 정했다가.. 아니면 돌아가서 다시 구하는 그리디 방식으로 풀 수 있을 것 같다.
