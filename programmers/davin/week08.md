# 8주차 알고리즘
## Network Delay Time
### 문제 풀이
1. 노드의 수 + 1 만큼 배열을 만든 후, 배열을 `Infinity`로 채운다. 해당 배열의 0번째와 K번째 요소에 0을 할당한다.
```javascript
[0,     Infinity,     0,      Infinity,     Infinity]
                    (K번째)
```
2. `while`문 내에서 `times`를 이용하여 반복문을 실행한다. K와 인접한 노드부터 차례대로 (K로부터의)딜레이 시간을 할당한다.
```javascript
[0,     1,      0,      1,      2]
      (딜레이) (K번째)  (딜레이)  (딜레이)
```
3. 딜레이 시간이 가장 긴 것을 반환한다.  
   K로부터 모든 노드가 신호를 받는 시간을 구해야 하므로, 신호를 가장 늦게 받는 노드가 신호를 받았다면 모든 노드가 신호를 받았음을 의미한다.


### 시간 복잡도
O(n log n)

### 제출 코드
```javascript
var networkDelayTime = function (times, N, K) {
  const array = new Array(N + 1).fill(Infinity);
  array[0] = 0;
  array[K] = 0

  let flag = true;

  while (flag) {
    flag = false;

    times.forEach(([u, v, w]) => {
      if (array[u] !== Infinity && array[v] > array[u] + w) {
        array[v] = array[u] + w;
        flag = true;
      }
    });
  }

  const result = Math.max(...array);
  return result === Infinity ? -1 : result;
};
```
