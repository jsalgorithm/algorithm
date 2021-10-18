# 10주차 알고리즘
## Contains Duplicate
### 문제 풀이 01
1. merge sort를 이용하여 배열을 정렬한다.
2. 정렬된 배열을 순회한다. 중복된 값이 있을 경우 true를 반환하고, 반복문을 마칠 때까지 true를 반환하지 못했다면 false를 반환한다.

### 시간 복잡도 01
merge sort의 시간 복잡도는 O(n log n)이지만 정렬 후 반복문을 이용하여 중복을 찾아내므로 O(n)

### 제출 코드 01
```javascript
const merge = (left, right) => {
  const result = [];
  
  while (left.length && right.length) {
    if (left[0] < right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  
  return [...result, ...left, ...right];
};

const mergeSort = (nums) => {
  if (nums.length === 1) {
    return nums;
  }
  
  const middle = Math.floor(nums.length / 2);
  const left = nums.slice(0, middle);
  const right = nums.slice(middle);
  
  return merge(mergeSort(left), mergeSort(right));
};

const containsDuplicate = function(nums) {
  const sorted = mergeSort(nums);
  
  for (let i = 0; i < sorted.length - 1; i++) {
    if (sorted[i]  === sorted[i + 1]) {
      return true;
    }
  }
  
  return false;
};
```

### 결과 01
![](../1mg/davin_contains_duplicate_01.png)

### 문제 풀이 02
1. `set`을 이용하여 중복 값을 제거한 객체를 생성한다.
2. 인자로 받은 `nums`의 length와 `set`의 size를 비교한다.

### 제출 코드 02
```javascript
var containsDuplicate = function(nums) {
  return new Set(nums).size < nums.length;
};
```

### 결과 02
![](../1mg/davin_contains_duplicate_02.png)
