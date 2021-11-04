## 다이나믹 프로그래밍 1번 문제

**LeetCode | Maximum Subarray**  
https://leetcode.com/problems/maximum-subarray/

### 문제풀이

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
