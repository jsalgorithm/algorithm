# Dynamic Programming

## 동적계획법

> 동적 계획법이란 복잡한 문제를 간단한 여러개의 문제로 나누어 푸는 방법을 말합니다.
>
> 부분 문제 반복과 최적 부분 구조를 가지고 있는 알고리즘을 적은 시간내에 풀 때 사용합니다.

* `최적부분구조` : 

  * 서울에서 부산까지 갈 때 최단거리를 구하는 방법을 생각해보자
  * (꼭 대구를 거쳐야 한다는 가정을 덧붙여보자)
  * 최단거리 = 서울에서 대구까지 가는 최단거리 + 대구에서 부산까지 가는 최단거리
  * 이처럼 전체를 해결하기위해 부분 문제를 최적 해결하는것을 의미한다.

  ![부산-서울 최단시간 경로](https://t1.daumcdn.net/cfile/tistory/99CC50445FB6684314)

  

  - `부분 문제 반복` :

    - 피보나치 계산의 구조를 보자

      ![피보나치 수열 효율적으로 구현하기 - 알고리즘닷컴](http://xn--299as6vb5i1je.com/files/2017/01/10/4c1d002d497853ab029d641536db54df)

    - 피보나치 문제를 재귀적으로 풀면, 반복해서 동일한 하위 문제들이 발생한다.
    - 다이나믹 프로그래밍의 핵심

  ---

  # 접근방법

  - 대표적인 다이나믹 프로그래밍 문제는 피보나치 수열 구하기 문제이다.
  - https://leetcode.com/problems/fibonacci-number/submissions/

  ## 상향식 문제풀이 (타뷸레이션)

  - 작은 하위 문제부터 살펴본 다음, 작은 문제의 정답을 이용해 큰 문제의 정답을 풀어간다.
  - Fibonacci(0), fibonacci(1)부터 풀이 해 나가는 방식

  ```javascript
  var fib = function (n) {
  	if (n <= 1) return n;
  
    let dp = [];
    dp[0] = 1;
      dp[1] = 1;
  
    for(let i = 2; i < n + 1; i++) {
      dp[i] = dp[i-1] + dp[i-2];
    }
      console.log(dp)
  
    return dp[n-1]
  };
  
  
  ```

  

  ## 하향식 문제풀이(메모이제이션)

  - 하위 문제에 대한 정답을 계산했는지 확인하며 문제를 풀어간다.
  - Fibonacci(100)을 구하기 위해 100번째 부터 거꾸로 계산하면서 해당하는 값이 계산 후 저장(메모)되어있는지 확인해 나가며 풀이

  ```javascript
  /**
   * @param {number} n
   * @return {number}
   */
  var fib = function (n) {
  	if (n <= 1) return n;
  	let dp = [];
  	if (dp[n]) return dp[n];
  
  	dp[n] = fib(n - 1) + fib(n - 2);
  
  	return dp[n];
  };
  ```

  ---

  

  

  

