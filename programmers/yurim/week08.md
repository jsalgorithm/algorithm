# 알고리즘 8주차

- 주제: 최단 경로, 이진 탐색 트리
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/09/27 ~ 10/03

## 목차

- 최단 경로

  - 문제 1) https://leetcode.com/problems/network-delay-time/
  - 문제 2) https://leetcode.com/problems/cheapest-flights-within-k-stops/

- 이진 탐색 트리
  - 문제 1) https://leetcode.com/problems/two-sum-iv-input-is-a-bst/
  - 문제 2) https://leetcode.com/problems/minimum-distance-between-bst-nodes/

# 최단 경로 문제 1 - 743. Network Delay Time

- 문제 분류: `최단경로`
- 문제 출처: [Leetcode - 743. Network Delay Time](https://leetcode.com/problems/network-delay-time/)
- 라벨: `Medium`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/135486506-f907b460-603a-4e21-9b42-7fc2e1810c58.png)

![image](https://user-images.githubusercontent.com/33214449/135486562-eada8913-2985-4b3e-9bfd-fdaf58dec5ca.png)

- 입력: 간선 정보(노드 관계와 가중치), 노드 개수, 출발 노드
  - 예를 들어 `n`(노드개수)가 4이면 1, 2, 3, 4라는 노드가 있는 것이다.
- 출력: 출발 노드 `k`에서 모든 노드로 신호를 보낸다고 할 때 걸리는 시간.

  - 모든 노드가 신호를 받지 못하는 경우(어떤 노드 하나라도 신호를 받지 못하는 경우) `-1`을 리턴하도록 한다.

- 노드 자기 자신으로 향하는 간선은 없다.
- 모든 간선은 유일하다. 예를 들어 (ui, vi)가 같은 경우는 없다.
- 음의 가중치는 없다고 가정한다.

## 풀이

- 처음 시도했던 접근법

  - times에 있는 간선(edge) 정보를 새로운 2차원 배열에 담고... 방문하지 않은 노드이면서 dist값이 최소인 노드를 골라서 dist를 갱신하고... 이렇게 무작정 다익스트라 알고리즘을 적용하려고 했는데 for문이 많이 중첩되서 그런지 시간초과가 나왔다.

실행 과정(벨만 포드 알고리즘 적용)

- `time`이라는 배열을 선언해 모두 `Infinity`값으로 초기화한다.
  - `time` 배열은 신호를 보내는 출발 노드인 `k`에서 각각의 i(인덱스) 노드로 가는 최소 시간을 담는 배열이다.
  - 노드는 1번부터 n번까지 있다. 그래서 편의상 `time` 배열의 인덱스 0번은 사용하지 않는다.
- 첫번째 for문: `n-1`번 반복한다.
  - 두번째 for문: `times` 배열에 든 간선 정보 개수만큼 반복한다.
    - `k -> v`로 가는 현재의 time값이 `k -> u로 가는 현재 최단 경로 값 + u와 v사이의 가중치`보다 클 경우, `time[v]`값을 갱신해준다. 그니까... 현재 간선을 거칠 때 더 빠른 시간에 신호를 보낼 수 있다면 경로값을 갱신해주는 것이다.
- 반복이 모두 완료되면, `time` 배열에는 출발 노드에서 각 노드로 가는 최단 길이(최소 통신 시간)가 잘 담겨져있을 것이다.
  - `time`배열에서 최댓값을 찾는다.(인덱스 0번은 제외하고 찾는다.) 최댓값을 찾는 이유는 k에서 신호를 동시에 보낸다고 할 때 가장 오래 걸리는 노드까지 통신이 끝나야 모든 노드에 신호가 보내졌다고 말할 수 있기 때문이다.
  - 최댓값이 Infinity라면 모든 노드가 신호를 받지 못한다는 뜻이다. 따라서 `-1`을 리턴한다. Infinity가 아니라면 정상적으로 동작한 것이기 때문에 찾은 최댓값을 리턴한다.

> 벨만 포드 알고리즘
>
> 첫번째 for문을 n-1번(정점의 개수 - 1) 반복하는 이유?
>
> 최단 경로에서 최대로 포함할 수 있는 간선의 개수는 n-1개이다.(모든 노드를 들리는 경우) 그러므로 어떠한 최단경로도 n-1개보다 간선이 많을 수 없을 것이다.
> s - v1 - v2 - vi - v 가 s에서 v로 가는 최단 경로라면, 첫번째 반복에서는 d(v1)이 확정될 것이고 두번째 반복에서는 d(v2)가 확정될 것이다.( d(v1)이 확정됐으니 ) 그래서 n-1번만 반복하면 모든 노드의 최단 경로가 확정되기에 충분하다.

```js
var networkDelayTime = function (times, n, k) {
  const time = Array(n + 1).fill(Infinity);

  time[k] = 0;
  for (let i = 0; i < n - 1; i++) {
    for (const [u, v, w] of times) {
      if (time[u] === Infinity) continue;
      if (time[v] > time[u] + w) time[v] = time[u] + w;
    }
  }

  let result = 0;
  for (let i = 1; i <= n; i++) {
    if (result < time[i]) result = time[i];
  }
  return result === Infinity ? -1 : result;
};
```

- 시간 복잡도: `O(NE)`
  - `(N-1)*E` -> N은 노드(정점)의 개수, E는 간선(edge)의 개수 = `times`의 length 를 의미한다.

![image](https://user-images.githubusercontent.com/33214449/135564425-4922e202-a6de-4dfe-8759-979b7069379a.png)

## Ref

- [Leetcode Discussion](https://leetcode.com/problems/network-delay-time/discuss/415157/Clean-JavaScript-Bellman-Ford-solution)

# 최단 경로 문제 2 - 787. Cheapest Flights Within K Stops

- 문제 분류: `최단경로`
- 문제 출처: [Leetcode - 787. Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/)
- 라벨: `Medium`, `JavaScript`

## 문제

- 입력:
  - `n`: n개의 도시를 의미. `n`이 3이라면 0,1,2 도시가 있는 것임
  - `flights`: `flight = [ [from, to, price], ... ]` from도시에서 to도시로 가는 price를 나타냄
- 출력:

  - `src` 출발지, `dst` 목적지, 최대 `k`번 정차할 때 가장 저렴한 price를 리턴하라.

- 간선의 개수: 1부터 n-1까지의 합 `(n*(n-1))/2`
- 음의 가중치는 없다고 가정한다. (price)
- 두 도시 사이에 겹치는 경로는 없다.
- 출발지(src) =/= 도착지(dst)

## 풀이

- 출발점에서 각각의 노드로 가는 최단 비용을 담게될 배열 `dist`를 선언하고, 배열 전체를 `Infinity`값으로 초기화해준다.
- 출발점의 dist는 0으로 초기화한다. `dist[src] = 0`
- 첫번째 for문을 도는데 k+1번만큼 돈다. (k번 정차한 최단 경로를 구하는 경우 k+1개의 간선을 거칠 것이기 때문이다. 그만큼은 반복해주어야한다.)
  - `temp` 배열을 선언하고 여기에 `dist` 배열 내용을 복사한다.(`slice`로 깊은 복사 실행)
  - 두번째 for문: 주어진 간선만큼 반복한다.(flights 배열을 돌면서)
    - dist[from] 값이 `Infinity`일 경우 스킵한다. (Infinity면 계산해봤자 갱신이 안됨)
    - 그렇지 않은 경우, `temp[to]`와 `dist[from] + price`중 작은 값을 가려 `temp[to]`를 갱신한다.
  - 내부 for문이 끝나면 dist 배열에 변경이 반영된 temp 배열을 복사한다.
  - 또 다시 첫번째 반복문을 돈다.
- 반복이 모두 끝나면 dist[dst], 즉 src에서 dst 도시로 가는 최저 비용(price)를 리턴한다. 만약 값이 Infinity라면 최단 비용이 없다는 뜻이므로 -1을 리턴하도록 한다.

- ➕ 첫번째 for문을 돌 때 dist와 temp는 같은 모습이지만 내부 for문이 진행되면서는 temp만 갱신된다. 그리고 내부 for문이 끝나면 dist를 temp값과 같도록 변경해준다.

> 📋 반복문마다 dist가 아닌 temp라는 배열을 갱신하는 이유
>
> temp라는 배열을 따로 선언해서 변화를 temp에 저장하는 이유는, 이제 막 생긴 변화를 바로 사용하고 싶지 않기 때문이다.(dist에 바로 갱신하면 어쩔 수 없이 그 변화값을 쓰게 된다.)
>
> 예를 들어 n=3, edge = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1 인 예제에서
>
> temp를 사용하지 않고 dist만 갱신하게 되면
>
> [0, 1, 100] 은 dist[1] = 100으로 값을 갱신하게되고
>
> [1, 2, 100] 은 dist[2] = 200으로 값을 갱신하게 된다. 하지만 이는 잘못된 결과이다. (k값에 따라서) 0개를 거쳐 가는 최단 경로를 찾아야하는데 이건 지금 0 -> 1 -> 2로 1개의 정류장을 거쳐가는 경로가 되기 때문이다. 이는 앞에서 갱신한 dist[1]을 즉각적으로 사용했기 때문이다. 따라서 dist를 직접 갱신하는 것이 아니라 temp를 갱신하도록 코드를 작성해주자.

```js
var findCheapestPrice = function (n, flights, src, dst, k) {
  let dist = Array(n).fill(Infinity);

  dist[src] = 0;

  for (let i = 0; i <= k; i++) {
    const temp = dist.slice();
    for (const [from, to, price] of flights) {
      if (dist[from] === Infinity) continue;
      temp[to] = Math.min(temp[to], dist[from] + price);
    }
    dist = temp.slice();
  }

  return dist[dst] === Infinity ? -1 : dist[dst];
};
```

- 시간 복잡도: O(kE)
  - `(k+1)*E` k는 문제에서 주어진 k. E는 간선의 개수를 의미

![image](https://user-images.githubusercontent.com/33214449/135590513-156847b7-4d42-4399-9c6a-008767605302.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/cheapest-flights-within-k-stops/discuss/662812/C%2B%2B-BFS-or-Bellman-Ford-Algo-or-Dijkstra-Algo)

# 이진 탐색 트리 문제 1 - 653. Two Sum IV - Input is a BST

- 문제 분류: `이진탐색트리`
- 문제 출처: [Leetcode - 653. Two Sum IV - Input is a BST](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/135724298-24fabc6d-50ae-497e-9c40-d86134f23b29.png)

- 입력: 이진탐색트리(`root`)와 `k`
- 출력: 이진탐색트리 내부에 두 개의 요소를 더하면 `k`값이 되는 경우가 존재할 경우 `true`를 리턴. 아닐 경우 `false`를 리턴

## 풀이

- `inorderBST()` 를 재귀적으로 실행: 먼저 중위순회로 주어진 이진탐색트리를 순회하며 배열에 노드들의 값을 저장한다. 배열에는 트리가 오름차순으로 정렬된 값이 담길 것이다.
- 위에서 얘기한 배열을 돌면서 더해서 k가 되는 두 요소를 찾는다. 요소 하나를 고정시키고(`fixed`) 이와 더하면 k가 되는 값을 `indexOf`로 찾는 방식이다.
  - 찾은 두 요소가 같은 인덱스에 위치하는 같은 값일 경우는 제외시킨다.

> Array.prototype.some()
>
> some() 메서드는 어떤 배열요소 하나라도 콜백함수가 true를 반환하는 경우가 있으면 true, 아니라면 false를 반환하는 메서드이다.

```js
var findTarget = function (root, k) {
  let arr = [];

  let inorderBST = function (root) {
    if (!root) {
      return;
    }

    inorderBST(root.left);
    arr.push(root.val);
    inorderBST(root.right);
  };

  inorderBST(root);

  let result = arr.some(function (fixed, index) {
    const findVal = k - fixed;
    if (arr.indexOf(findVal) !== -1 && arr.indexOf(findVal) !== index) {
      return true;
    }
  });

  return result;
};
```

- 시간 복잡도: `O(n^2)`
  - 모든 노드를 돌며(`O(n)`) indexOf로 값을 찾기 때문에(`O(n)`) 최악의 경우 시간 복잡도는 `O(n^2)`이다.

![image](https://user-images.githubusercontent.com/33214449/135724291-6f429216-1063-4dfb-bed2-5016e0d1d6ac.png)

## Ref

- [자바스크립트 Array 메소드 및 예제에 대한 시간 복잡도 Big O](https://kimyejin.tistory.com/m/62)

# 이진 탐색 트리 문제 2 - 783. Minimum Distance Between BST Nodes

- 문제 분류: `이진탐색트리`
- 문제 출처: [Leetcode - 783. Minimum Distance Between BST Nodes](https://leetcode.com/problems/minimum-distance-between-bst-nodes/)
- 라벨: `Easy`, `JavaScript`

## 문제

## 풀이

```js

```

- 시간 복잡도:
