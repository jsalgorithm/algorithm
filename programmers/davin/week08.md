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

## Cheapest Flights Within K Stops
### 문제 풀이
1. 노드의 수 + 1 만큼 배열을 만든 후, 배열을 `Infinity`로 채운다. 해당 배열의 `src` 번째 요소에 0을 할당한다. (시작 지점에 0 할당)
2. k 만큼 노드를 거쳐갈 수 있으므로 k를 이용하여 반복문을 돈다.
3. `flights`를 이용하여 반복문을 돈다. `flights`의 j 번째 배열을 이용하여 이동 비용을 계산하고, 이미 계산된 값보다 더 작은 경우 재할당한다.
4. `dst` 번째로 이동이 가능하다면 array의 `dst` 번째 요소(비용)를 반환하고, 이동이 불가능하다면 -1을 반환한다.

### 시간 복잡도
O(n log n)

### 제출 코드
```javascript
var findCheapestPrice = function(n, flights, src, dst, k) {
  let array = new Array(n + 1).fill(Infinity);
  array[src] = 0;
  
  for(let i = 0; i < k + 1; i++){
    const copy = [...array];

    for(let j = 0; j < flights.length; j++){
      const [from, to, price] = flights[j];
      copy[to] = Math.min(copy[to], array[from] + price);
    }

    array = [...copy];
  }
  
  return array[dst] === Infinity ? -1 : array[dst];
};
```

__참고__
[알고리즘 - 다익스트라 알고리즘(Dijkstra's algorithm) : 모든 정점까지의 최단 경로 구하기
](https://chanhuiseok.github.io/posts/algo-47/)
