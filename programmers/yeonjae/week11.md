# Dynamic Programing

- 문제 : https://leetcode.com/problems/maximum-subarray/

- 코드:

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const maxSubArray = function (nums) {
	let sum = [];
	sum[0] = nums[0];
	for (let i = 0; i < nums.length - 1; i++) {
		if (sum[i] < 0) {
			sum.push(nums[i + 1]);
		} else {
			sum.push(nums[i + 1] + sum[i]);
		}
	}
	return Math.max(...sum);
};
/**
 * 계속해서 누적 값을 더하면서
 * (누적값) + (새로운값) 의 결과가 음수가 된다면, 굳이 결과값을 subArray에 넣을 필요가 없어진다.
 * 따라서 새로운 값에서부터 다시 누적값을 계산한다.
 * 최종적으로 sum 배열에서의 최대값이 연속적인 값의 합 중 가장 큰 값이 된다.
 */+

```

- 풀이내용:
  - 주어진 nums 배열 내의 연속적인 값들을 누적해서 더한 값 중 가장 큰 값을 리턴하는 문제
  - 연속적인 값을 더했을 때, 음수가 된다면 그 다음 반복문에서는 리셋 후 새로 누적값을 계산한다
    - `[-1, -3] `: -1 + -3 = -4
      - 음수끼리의 합으로 인해, 누적값이 최대값이 될 가능성이 없어졌음
    - `[1, 1, -3]`: 1 + 1 = 2
      -  2 - 3 = -1
      - 누적값이 음수가 된 순간 subArray의 합이 최대값이 될 가능성이 없어졌다.
      - 따라서 해당 결과값(-1)까지의 누적값을 초기화하고 새로운 subArray의 가능성을 찾는다. 
- 시간복잡도: O(n)

### kadane

- 해당 문제는 카데인 알고리즘으로도 풀 수 있다.
- 카데인 알고리즘이란 각 단계마다 최댓값을 담아 어디서 끝나는지 찾는 방식으로 풀이하는 방법이다.

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const maxSubArray = function (nums) {
	let best_sum = Number.MIN_VALUE;
	let current_sum = 0;

	for (let num of nums) {
		current_sum = Math.max(num, num + current_sum);
		best_sum = Math.max(current_sum, best_sum);
	}

	return best_sum;
};
```

---

- 문제: https://leetcode.com/problems/climbing-stairs/
- 코드:

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
	let dp = [];
	dp[0] = 1;
	dp[1] = 1;
	for (let i = 2; i < n + 1; i++) {
		dp[i] = climbStairs(dp[i - 1]) + climbStairs(dp[i - 2]);
	}

	return dp[n - 1];
};
```

- 풀이내용:
  - 문제의 내용만 다르지 규칙을 확인 후 점화식을 세워보면 피보나치 수열이다.
- 시간복잡도: ?

