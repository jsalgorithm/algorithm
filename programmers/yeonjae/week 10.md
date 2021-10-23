# Week 10

## 분할정복

### 다중 분기 재귀를 기반으로 하는 알고리즘 디자인 패러다임을 말한다.

- 분할정복은 문제를 분할해서 정복한 후, 정답을 조합해 나가는 방식으로 풀이한다.

---

- 문제 : https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

- 코드

  ```javascript
  /**
   * @param {number[]} prices
   * @return {number}
   */
  var maxProfit = function (prices) {
  	let min_price = Number.MAX_VALUE;
  	let profit = 0;
  
  	for (let price of prices) {
  		console.log(price);
  		min_price = Math.min(min_price, price);
  		profit = Math.max(profit, price - min_price);
  	}
  
  	return profit;
  };
  
  
  ```

  

- 풀이내용

  - 분할정복으로 풀지 못해서 최소값과 최대값을 매 반복문마다 적절하게 변경하는 방식으로 풀이했다.
  - 최소값을 javascript의 최대값인 Number.MAX_VALUE 로 설정해 준 뒤, prices의 값과 비교하여 작은 값으로 교체한다.
  - 최대값을 0으로 할당한 뒤, prices의 값과 비교하여 큰 값으로 교체한다.

- 시간복잡도

  - Math.min, Math.max 는 각각 O(N)만큼의 시간복잡도를 필요로한다.
  - 따라서 총 시간복잡도는 O(N^2)

---

- 문제 : https://leetcode.com/problems/contains-duplicate/

- 코드

  ```javascript
  /**
   * @param {number[]} nums
   * @return {boolean}
   */
  const containsDuplicate = function(nums) {
      return new Set(nums).size < nums.length;
  };
  ```

  

- 풀이내용

  - 분할정복으로 풀지 못해서 set 자료구조를 이용했다.
  - javascript의 set은 배열 내에서 유일한 값만을 저장한다.
  - 만약 set의 size보다 배열의 길이가 길다면, 중복된 값이 있음을 알 수 있다.

- 시간복잡도

  - O(n), set자료구조의 시간복잡도는 선형적이다.

----

## 그리디 알고리즘

### 그리디 알고리즘이 잘 적용되는 문제는, 탐욕 선택 속성을 갖고있는 최적 부분구조 문제들이다.

- 탐욕선택속성 : 앞의 선택이 이후 선택에 영향을 주지 않는 것을 의미
- 최적 부분 구조 : 문제의 최적 해결 방법이 부분 문제에 대한 최적 해결 방법으로 구성되는 경우
- 배낭문제, 동전바꾸기 문제 등이 대표적인 그리디 알고리즘 문제

---

- 문제: https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

- 코드

  ````javascript
  /**
   * @param {number[]} prices
   * @return {number}
   */
  const maxProfit = function (prices) {
  	let money = 0;
  	for (let i = 0; i < prices.length; i++) {
  		if (prices[i + 1] > prices[i]) {
  			money += prices[i + 1] - prices[i];
  		}
  	}
    return money
  };
  
  ````

- 풀이내용

  - 기간 내내 샀다가 팔 수 있으므로 현재의 값보다 큰 값인 경우 무조건 팔면된다.
  - 따라서 매 일 마다 주식을 사고 팔아 이익을 취하는 형태로 코드를 짠다.

- 시간복잡도

  - O(N)

---

- 문제 : https://leetcode.com/problems/assign-cookies/

- 코드

  ```javascript
  var findContentChildren = function(g, s) {
      g.sort((a,b) => a-b);
      s.sort((a,b) => a-b);
      let j = 0, res = 0;
      for (let num of s) {
          if (num >= g[j]) res++, j++;
      }
      return res;
  };
  ```

- 풀이내용

  - 그리드팩터의 크기보다 큰 쿠키만 받을 수 있다.
  - 각각 주어진 쿠키 사이즈와 그리드팩터를 정렬한 다음
  - 해당 쿠키의 사이즈를 순회하며 그리드팩터보다 큰 경우 res++한다.

- 시간복잡도

  - O(n)

