# Dynamic programming
## 53. Maximum Subarray
 

### 코드
 
```
var maxSubArray = function(nums) {
    for(let i = 1; i < nums.length; i++){
        nums[i] = Math.max(nums[i], nums[i]+nums[i-1]);
    }
    return Math.max(...nums)
};
```

### 문제풀이

1. 반복문을 돌면서 nums[i]의 값과 nums[i]+nums[i-1]을 비교

2. 둘중에 큰 값을 num[i]에 넣어준다.

3. 이 배열중에 가장 큰 값을 반환
