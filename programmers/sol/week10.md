## 분할 정복 1번 문제

**LeetCode | Contains Duplicate**  
https://leetcode.com/problems/contains-duplicate/

#### 방법 1: set 객체

### 문제풀이

Set 객체를 이용하여 nums 배열의 중복을 제거한 다음 기존의 nums 배열과 같은지 비교한다.

### 코드

```javascript
/**
 * @param {number[]} nums
 * @return {boolean}
 */
const containsDuplicate = function (nums) {
	let set = new Set(nums);

	return nums.length === [...set].length ? false : true;
};
```

### 시간복잡도

O(n)

#### 방법 2: 정렬

### 문제풀이

1. nums 배열을 오름차순 정렬한 뒤 sortedNums 변수에 할당한다.
2. sortedNums 배열을 순회하면서 i번째와 i+1번째 원소를 비교한다.
3. i번째와 i+1번째 원소가 같으면 중복값이 존재한다는 의미이므로 true를 반환한다.
4. 중복값이 없으면 false를 반환한다.

### 코드

```javascript
const containsDuplicate = function (nums) {
	const sortedNums = nums.sort();

	for (let i = 0; i < sortedNums.length - 1; i++) {
		if (sortedNums[i] === sortedNums[i + 1]) return true;
	}
	return false;
};
```

### 시간복잡도

O(n log n)

---

## 분할 정복 2번 문제

**LeetCode | Best Time to Buy and Sell Stock**  
https://leetcode.com/problems/best-time-to-buy-and-sell-stock/

### 문제풀이

`stock의 구매일과 판매일의 차액(=이익)이 가장 큰 날을 구하는 것이 포인트!`

1. 이익의 초기값을 0, prices 배열의 첫 번째 인덱스를 최솟값 min으로 잡는다.
2. prices 배열을 두 번째 인덱스(1)부터 순회한다.
3. prices[i]와 현재 최솟값 min 중 더 작은 값을 다시 min에 할당한다.
4. 현재의 이익과 prices[i]에서 현재의 최솟값 min을 뺀 값(새로운 이익) 중 더 큰 값을 다시 profit에 할당한다.
5. 최종적인 이익인 profit을 반환한다.

### 코드

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
const maxProfit = function (prices) {
	let profit = 0;
	let min = prices[0];
	for (let i = 1; i < prices.length; i++) {
		min = Math.min(prices[i], min);
		profit = Math.max(profit, prices[i] - min);
	}
	return profit;
};
```

### 시간복잡도

---

## 그리디 알고리즘 1번 문제

**LeetCode | Best Time to Buy and Sell Stock II**  
https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/

### 문제풀이

`stock의 가격이 당일보다 익일에 더 비싸면 판매하는 것이 포인트!`

1. 이익의 초기값을 0으로 잡는다.
2. prices 배열을 두 번째 인덱스(1)부터 순회한다.
3. prices[i]가 prices[i-1]보다 크면, 즉 익일의 가격이 당일보다 비싸면 profit에 prices[i]에서 prices[i-1]을 뺀 값을 더한다.
4. 누적된 이익인 profit을 반환한다.

### 코드

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
const maxProfit = function (prices) {
	let profit = 0;
	for (let i = 1; i < prices.length; i++) {
		if (prices[i] > prices[i - 1]) profit += prices[i] - prices[i - 1];
	}
	return profit;
};
```

### 시간복잡도

O(n)

---

## 그리디 알고리즘 2번 문제

**LeetCode | Assign Cookies**  
https://leetcode.com/problems/assign-cookies/

### 문제풀이

`아이들이 만족할 만한 쿠키 사이즈 중 가장 작은 것을 나눠주는 것이 포인트!`

1. g 배열과 s 배열을 오름차순으로 정렬한다.
2. 쿠키를 나눠줄 수 있는 아이의 수인 count를 0, s 배열의 인덱스 cookie를 0, g 배열의 인덱스 child를 0으로 초기화한다.
3. child가 g.length보다 작으면서 cookie가 s.length보다 작을 때까지 while문으로 순회한다.
4. s[cookie] >= g[child], cookie번째 쿠키의 사이즈가 child번째 아이가 만족할 만한 쿠키의 사이즈보다 크거나 같으면 count, cookie, child 모두 1씩 증가시키고 while문을 계속 진행한다.
5. 위의 조건을 만족하지 않으면 cookie를 1씩 증가시킨다. (= 다음 쿠키 사이즈로 넘어간다.)
6. 최종적으로 쿠키를 나눠줄 수 있는 아이의 수인 count를 반환한다.

### 코드

```javascript
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
const findContentChildren = function (g, s) {
	g.sort((a, b) => a - b);
	s.sort((a, b) => a - b);

	let count = 0;
	let cookie = 0;
	let child = 0;

	while (child < g.length && cookie < s.length) {
		if (s[cookie] >= g[child]) {
			count++;
			cookie++;
			child++;
			continue;
		}
		cookie++;
	}
	return count;
};
```

### 시간복잡도

O(n2)

### 참고자료

https://earth-95.tistory.com/22
