# 최단경로

![GPS 네비게이션 응용 프로그램, 자기 나침반, 펜, 선택적 포커스 효과 디자인으로 세계지도에 압정의 그룹과 현대 검은 광택의 터치  스크린 스마트 폰의 모바일 GPS 네비게이션, 여행, 관광 개념 매크로보기는 내 자신의 로열티 무료](https://previews.123rf.com/images/scanrail/scanrail1309/scanrail130900029/22441102-gps-%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%EC%85%98-%EC%9D%91%EC%9A%A9-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8-%EC%9E%90%EA%B8%B0-%EB%82%98%EC%B9%A8%EB%B0%98-%ED%8E%9C-%EC%84%A0%ED%83%9D%EC%A0%81-%ED%8F%AC%EC%BB%A4%EC%8A%A4-%ED%9A%A8%EA%B3%BC-%EB%94%94%EC%9E%90%EC%9D%B8%EC%9C%BC%EB%A1%9C-%EC%84%B8%EA%B3%84%EC%A7%80%EB%8F%84%EC%97%90-%EC%95%95%EC%A0%95%EC%9D%98-%EA%B7%B8%EB%A3%B9%EA%B3%BC-%ED%98%84%EB%8C%80-%EA%B2%80%EC%9D%80-%EA%B4%91%ED%83%9D%EC%9D%98-%ED%84%B0%EC%B9%98-%EC%8A%A4%ED%81%AC%EB%A6%B0-%EC%8A%A4%EB%A7%88%ED%8A%B8-%ED%8F%B0%EC%9D%98-%EB%AA%A8%EB%B0%94%EC%9D%BC-gps-%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%EC%85%98-%EC%97%AC%ED%96%89-%EA%B4%80.jpg)

가장 짧은 경로, 비용이 가장 적은 경로를 탐색하는 알고리즘입니다.

흔히 인공위성, GPS 소프트웨어에서 실제로 가장 많이 사용되는 알고리즘입니다.

하나의 정점에서 다른 모든 정점으로 가는 최단 경로를 알려줍니다.

단, 음의 간선을 포함할 수 없습니다. 하지만 현실세계에서 음의 간선은 존재하지않기 때문에 현실세계에 적합한 알고리즘입니다

----

### 다익스트라 알고리즘은 다이나믹 프로그래밍 문제인 이유?

- 최단거리는 여러개의 최단 거리로 이루어져 있기 때문
- 작은 문제가 큰 문제 속에 비슷한 형태로 포함되어있는 다이나믹 프로그래밍 유형 중 하나라고 볼 수 있음

하나의 최단거리를 구할 때 그 이전까지 구했던 최단 거리 정보를 그대로 사용한다는 특징이 있음

----

다익스트라 알고리즘은 현재까지 알고있던 최단 경로를 계속해서 갱신하며 진행합니다.

예를들어, 아래와 같은 그래프의 최단경로를 찾고자 할 때 먼저 각 정점에서 다음 정점까지의 최단거리를 구합니다.

![djikstra01.png](https://github.com/jsalgorithm/algorithm/blob/main/docs/img/djikstra01.png?raw=true)

이후 각 정점에서 최단거리끼리의 합을 구하면 모든 노드를 지나치는 최단거리를 구할 수 있습니다.

모든 노드를 지나치는 최단거리를 구하는 방법은 아래와 같습니다.

1. x,y,z에서 출발할 때 이웃한 정점까지 필요한 비용을 계산합니다.

   ![djikstra02.png](https://github.com/jsalgorithm/algorithm/blob/main/docs/img/djikstra02.png?raw=true)

2. 다음 노드로 이동하면서 최단경로로 업데이트합니다.

   1. X ->  Z 의 경우, Y를 거치면 5 만 소비되기 때문에 업데이트 합니다.

   2. Z -> X 의 경우, Y를 거치면 5만 소비되기 때문에 업데이트합니다.

      ![djikstra03.png](https://github.com/jsalgorithm/algorithm/blob/main/docs/img/djikstra03.png?raw=true)

3. 각각의 테이블에서, 새로운 정보를 업데이트합니다.

   ![djikstra.04.png](https://github.com/jsalgorithm/algorithm/blob/main/docs/img/djikstra.04.png?raw=true)

   1. x에서 이동하는 경우는 모두 최단거리이므로 최종값입니다.
   2. y에서 이동하는 경우는 모두 최단거리이므로 최종값입니다.
   3. z에서 이동하는 경우는 모두 최단거리이므로 최종값입니다.

4. 모든 테이블에 최단거리로 업데이트되었습니다. 완성된 테이블이 해당 정점에서부터 나머지 정점까지의 최단 경로입니다.

- 이 방법은 구한 배열을 매 번 탐색해서 가장 짧은 거리를 찾는 방법으로 쓰입니다.
- 시간복잡도는 O(N^2)으로 형성됩니다.
- 더 빠른 동작을 원한다면 힙 구조를 사용하여 풀이해야합니다.



