# Week 08

## 최단경로

- 문제 : https://leetcode.com/problems/network-delay-time/

  > 1~n 까지의 노드, 이동하는데 걸리는 시간(time), 간선간의 이동 거리에 대한 정보` times[i] = (ui, vi, wi) `가 주어진다. 
  >
  > k정점에서 출발해서  n개의 노드가 신호를 받을 수 있는 시간을 리턴하라. 단 불가능한 경우 -1을 리턴한다.

  

- Code:

```javascript
/**
 * times = 각 정점까지에 대한 가중치 정보를 담은 list
 * n = 모든 정점의 갯수
 * k = 시작 정점
 */

const networkDelayTime = function (times, n, k) {
	let distance = Array(n + 1).fill(Infinity);
	distance[k] = 0;
	for (let i = 0; i < n; i++) {
		for (const [u, v, w] of times) {
			if (distance[u] === Infinity) continue;
			if (distance[v] > distance[u] + w) {
				  distance[v] = distance[u] + w;
			}
		}
	}

	let res = 0;
  for (let i = 1; i <= n; i++) {
    res = Math.max(res, distance[i]);
  }
  return res === Infinity ? -1 : res;
};
```

- 풀이내용:
  - `distance`  경로에 대한 정보를 담을 Array를 생성합니다.
    - 시작노드k에서부터 각 노드까지의 거리를 담은 배열입니다.
    - 현재, 모든 경로에 대한 정보가 없으므로 무한대 처리합니다.
    - n+1 해주는 이유는 뒤에서 사용 할 노드숫자를 편하게 쓰기 위함입니다.
    -  ex : k 가 1로 주어졌을 때 그대로 대입해서 사용하기위함.
  - 시작노드인 `k`에서 k까지의 이동거리는 0이므로 0을 할당합니다.
  - 주어진 node의 개수만큼 반복문을 시행합니다. 모든 정점에 대한 경로를 확인합니다.(times가 이중배열이라..)
    - times 배열의 행의 값들을 각각 `u,v,w` 에 할당합니다.
    - 출발지에 존재하는 경로가 무한대이면, 넘어갑니다.
    - 출발지에 존재하는 경로가 있다면, 주어진 times의 배열에 있는 정보로, 도착지까지의 경로가 새로운 최단거리로 업데이트 될 지 여부를 따집니다.
      - `distacne[v]`기존의 경로
      - `distance[u] + w` 갱신될 수 있는 새로운 경로
      - 최종적으로, times배열을 모두 순회하면 주어진 경로에 대한 최단거리 배열을 만들 수 있습니다.
  - 최종값을 구할 때, 0번째 값은 무한대이므로 제외하고 계산합니다.

- Example

- ![img](https://assets.leetcode.com/uploads/2019/05/23/931_example_1.png)

  ```
  Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
  Output: 2
  ```

  1. [∞,∞,∞,∞,∞,∞]
  2. [∞,∞,0,∞,∞]
  3. [∞,(0+1),0,∞,∞]
  4. [∞,1,0,(0+1),∞]
  5. [∞,1,0,1,(1+1)]
  6. [∞,1,0,1,2] <- 최종 최단경로 

  | **52 / 52** test cases passed.               | Status: Accepted |
  | -------------------------------------------- | ---------------- |
  | Runtime: **116 ms**Memory Usage: **46.5 MB** |                  |

  ----

- 문제: https://leetcode.com/problems/cheapest-flights-within-k-stops/

> 시작점에서 도착점까지의 가장 저렴한 가격을 계산한다. 단, k번 이내로 도착해야한다.
>
> 불가능한 경우 -1을 리턴한다... 

- Code:

  ```javascript
  const findCheapestPrice = function (n, flights, src, dst, k) {
  	let prices = new Array(n).fill(Infinity);
  	prices[src] = 0;
  
  	for (let i = 0; i < k + 1; i++) {
  		const tempPrice = [...prices];
  		for (let [s, d, p] of flights) {
  			if (prices[s] === Infinity) continue;
  			if (prices[s] + p < tempPrice[d]) {
  				tempPrice[d] = prices[s] + p;
  			}
  		}
  		prices = tempPrice;
  	}
  	return prices[dst] === Infinity ? -1 : prices[dst];
  };
  ```

  - Runtime: 166 ms, faster than 38.58% of JavaScript online submissions for Cheapest Flights Within K Stops.

    Memory Usage: 44.5 MB, less than 50.39% of JavaScript online submissions for Cheapest Flights Within K Stops.

  - 풀이내용 : 위 문제와 비슷..

  - 단 노드에 들릴 수 있는 횟수가 k번으로 제한되어있으므로 반복문에서 제한을 걸어준다.

- example

  ```
  Input: n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
  Output: 200
  Explanation: The graph is shown.
  The cheapest price from city 0 to city 2 with at most 1 stop costs 200, as marked red in the picture.
  ```

  

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/02/16/995.png)

