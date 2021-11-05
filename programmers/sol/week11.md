## 다이나믹 프로그래밍 1번 문제

**LeetCode | Maximum Subarray**  
https://leetcode.com/problems/maximum-subarray/

### 문제풀이

`카데인 알고리즘 => 현재 부분배열의 합은 이전 부분배열의 합 + 현재 인덱스의 값`

1. 두 번째 인덱스부터 시작하면서 nums 배열을 순회
2. 현재 인덱스 값과 이전 부분배열의 합 중에서 더 큰 값으로 인덱스 값 변경
   ❗️이전 부분배열의 합이 현재 인덱스 값보다 작으면 굳이 현재 부분배열의 합을 구할 필요 X
3. nums 배열 중에서 가장 큰 값을 반환

![카데인 알고리즘 참고 사진](https://miro.medium.com/max/2100/1*0T4vufD3IKkBLC895NNtkA.png)

### 코드

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const maxSubArray = function (nums) {
	// O(n)
	for (let i = 1; i < nums.length; i++) {
		// 현재 인덱스 값과 이전의 최대 부분배열합 중 더 큰 값으로 인덱스 값 변경
		nums[i] = Math.max(nums[i], nums[i] + nums[i - 1]); // O(n)
	}
	return Math.max(...nums);
};
```

### 시간복잡도

O(n^2)

### 참고자료

https://medium.com/@vdongbin/kadanes-algorithm-%EC%B9%B4%EB%8D%B0%EC%9D%B8-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-acbc8c279f29

---

## 다이나믹 프로그래밍 2번 문제

**LeetCode | Climbing Stairs**  
https://leetcode.com/problems/climbing-stairs/submissions/

### ⭐️ 탑다운 방식

### 문제풀이

`피보나치 수열`

1. 메모이제이션을 위해 빈 배열 dp 생성 후 0번째, 1번째 인덱스 값을 1로 설정
2. n이 1인 경우, 1을 반환 => 기본 단계
3. 피보나치 수열 함수 fibo 구현

- dp[n]이 이미 계산된 값이라면 그대로 반환
- 아직 계산하지 않는 값이라면 fibo(n - 1) + fibo(n - 2) 값을 dp[n]에 할당하고 반환

4. 최종적으로 fibo(n) 반환

![피보나치 수열 알고리즘 참고 사진](https://t1.daumcdn.net/cfile/tistory/99B94B4D5BDEAF3B14)

### 코드

```javascript
/**
 * @param {number} n
 * @return {number}
 */
const climbStairs = function (n) {
	let dp = [1, 1]; // 메모이제이션

	if (n === 1) return 1; // 기본 단계

	function fibo(n) {
		if (dp[n] !== undefined) return dp[n]; // 이미 계산한 부분
		return (dp[n] = fibo(n - 1) + fibo(n - 2)); // 아직 계산하지 않은 부분
	}
	return fibo(n);
};
```

### ⭐️ 바텀업 방식

### 문제풀이

1. 메모이제이션을 위해 빈 배열 dp 생성 후 0번째, 1번째 인덱스 값을 1로 설정
2. 2번째 인덱스부터 for문 순회

- dp[i - 1] + dp[i - 2]값을 dp[i]에 할당

3. 최종적으로 dp[n]값 반환

### 코드

```javascript
const climbStairs = function (n) {
	let dp = [];
	dp[0] = 1; // 초기값 세팅
	dp[1] = 1;

	for (let i = 2; i <= n; i++) {
		dp[i] = dp[i - 1] + dp[i - 2];
	}
	return dp[n];
};
```

### 시간복잡도

O(n)

### 참고자료

나동빈, ⌜이것이 취업을 위한 코딩 테스트다⌟, 한빛미디어, 2020
