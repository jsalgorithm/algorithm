# 분할정복
## 217. Contains Duplicate

### 코드

```javascript
const containsDuplicate = (nums) => {
    const set = new Set(nums);
    return set.size !== nums.length;
};
```


### 문제풀이

1\. 중복하지 못하게 set에 배열을 넣어준다.

2\. 중복값이 있다면 set의 크기와 기존배열의 크기가 다르다. 이것을 사용해서 boolean값을 반환함



## 121. Best Time to Buy and Sell Stock

### 코드

```javascript
var maxProfit = function(prices) {
    
    let maxProfit = 0; //1
    let min = prices[0]; //2
    
    for(let i = 1; i < prices.length; i++) { //3
        min = Math.min(prices[i], min);
        maxProfit = Math.max(maxProfit, prices[i] - min); //4
    }
    return maxProfit;
};
```


### 문제풀이

1\. maxProfit에 초기값 설정.

2\. min(최소값)에 대한 초기값을 설정

3\. 반복하면서 min에 대한 가장 최근값을 다음요소와 비교하고

    비교한 값중에 작은 값을 min의 새 값으로 설정해주기(==Math.min()이용)

4.maxPofit의 이전값 또는 현재 가격에서 min을 뺀 최대한 이익도 업데이트해준다.
