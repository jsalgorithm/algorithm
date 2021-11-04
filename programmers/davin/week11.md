# 11주차 알고리즘
## Maximum Subarray
### 문제 풀이
1. `nums` 배열을 변형시켜야 하므로 복사본 `copy`를 선언한다.
2. 반복문을 이용하여 `copy`를 순회한다. `i`는 1부터 시작한다.
3. `sum`을 선언하고, `i`번째 숫자와 `i - 1`번째 숫자를 더한 값을 할당한다.
4. `sum`과 `i`번째 숫자를 비교한 후, 더 큰 값을 `i`번째에 할당한다.
5. `copy` 배열에서 가장 큰 값을 반환한다.

```
[ i를 1부터 시작한 이유 ]
0번째 숫자는 i - 1번째 값을 구할 수 없으므로 1부터 시작한다.

[ i번째 숫자와 i - 1번째 숫자를 더하는 이유 ]
누적된 값을 구하는 과정이다.
예를 들어 5, 3, 1인 경우 반복문을 끝까지 돌았다면 5, 8, 9가 된다. 0번째 이후의 값들은 누적된 값을 가지게 된다.
예를 들어 5, -10, 1인 경우 반복문을 끝까지 돌았다면 5, -5, 1이 된다. -5 + 1보다 1이 더 크기 때문에 이 경우 값을 바꾸지 않는다.

[ 더한 값과 i번째 숫자를 비교하는 이유 ]
더한 값이 원래 값보다 작은 경우 더하지 않는 것이 더 나으므로 숫자가 더 커졌을 때만 할당한다.
예를 들어 -2, 1인 경우 이 둘은 더하지 않고 1을 반환하는 것이 맞다.
```

### 시간 복잡도
O(n2)

### 제출 코드
```javascript
const maxSubArray = function(nums) {
  const copy = nums.slice();

  for (let i = 1; i < copy.length; i++){
    const sum = copy[i] + copy[i - 1];
    copy[i] = Math.max(copy[i], sum);
  }

  return Math.max(...copy);
};
```

## Climbing Stairs
### 문제 풀이
1. 계단이 1개일 경우 오르는 방법은 1개이고, 계단이 2개일 경우 오르는 방법은 2개이므로 `n`이 3보다 작으면 `n`을 반환한다.
2. `n`이 3 이상일 경우 연산 결과를 저장할 `cache`를 선언한다. key는 계단의 수, value는 계단을 오르는 방법의 수로 저장한다.
3. `getCache` 재귀 함수를 선언하여 `n`과 `cache`를 인자로 넣고 실행한다.
4. `cache`에 저장된 값이 없을 경우 계산하여 저장한다. 계산 공식은 아래를 사용한다. (피보나치 수열)
```
F(n) = F(n - 1) + F(n - 2)
```
5. 캐시된 값이 있는 경우 다시 계산할 필요가 없으므로 캐시된 값을 반환한다.
6. 최종 결괏값을 반환한다.

### 제출 코드
```javascript
function getCache(n, cache) {
  if (!!cache[n]) {
    return cache[n];
  }
  
  cache[n] = getCache(n - 1, cache) + getCache(n - 2, cache);
  
  return cache[n];
}

function climbStairs(n) {
  if (n < 3) {
    return n;
  }
  
  const cache = { 1: 1, 2: 2 };

  return getCache(n, cache);
};
```
