# 9주차 알고리즘
## Longest Repeating Character Replacement
### 문제 풀이
1. 창문의 범위를 지정하기 위해 `left`와 `right`를 선언한다. 초깃값은 둘 다 0으로 지정한다.
2. 창문의 범위 내에서 제일 많이 등장한 알파벳의 수를 저장하기 위해 `maxCharCount`를 선언한다. 초깃값은 0으로 지정한다.
3. 창문의 범위 내에서 알파벳의 수를 저장하기 위해 `visited`를 기록한다.
4. `right`(창문의 끝)가 `s`의 길이만큼 커질 때까지 `while` 문을 돈다. `right`는 반복문을 돌 때마다 1씩 커지도록 한다.
5. `right` 번째 알파벳의 등장 횟수를 `visited`에 기록하고, 창문 범위 내에서 가장 많이 등장했다면 `maxCharCount`를 업데이트한다.
6. 현재 범위의 알파벳 수 - 현재 범위에서 가장 많이 등장한 알파벳의 수 = **변경되어야 할 알파벳의 수**가 주어진 `k`보다 크다면 `left`를 증가시켜 창문을 오른쪽으로 이동시킨 후, `visited`에서 `left` 번째 알파벳의 수를 1 감소시킨다. (창문을 오른쪽으로 이동시키면서 첫 번째 알파벳을 잘라냈으므로)
7. 반복문을 모두 종료한 후, `right` - `left`(창문의 범위)를 반환한다.

### 시간 복잡도
O(n)

### 제출 코드
```javascript
const characterReplacement = (s, k) => {
  let left = 0;
  let right = 0;
  let maxCharCount = 0;
  const visited = {};

  while (right < s.length) {
    const char = s[right];
    visited[char] = visited[char] ? visited[char] + 1 : 1;

    if (visited[char] > maxCharCount) maxCharCount = visited[char];

    if (right - left + 1 - maxCharCount > k) {
      visited[s[left]]--;
      left++;
    }

    right++;
  }

  return right - left;
};
```

## Contains Duplicate II
### 문제 풀이
1. 인덱스를 저장하기 위한 `obj`를 선언한다.
2. `nums`의 길이만큼 반복문을 돈다.
3. `obj`에 인덱스가 저장되어 있지 않다면(처음으로 등장한 숫자라면) 연산할 값이 없으므로 `obj`에 인덱스를 저장한다.
4. `obj`에 인덱스가 저장되어 있다면(중복으로 등장한 숫자라면) 저장된 인덱스를 가져와 절댓값을 구한다.
5. 이 절댓값이 `k`보다 작거나 같다면 true를 반환한다. 만약 이 절댓값이 `k`보다 크다면 `obj`의 인덱스를 업데이트한다.  
   `obj`의 인덱스를 업데이트하는 이유 연산된 절댓값이 `k`보다 작거나 같으려면 인덱스 `i`와 `j`의 차이가 커지면 안 된다. 따라서 절댓값이 조건에 충족하지 못한다면 `obj`에 저장된 인덱스의 크기를 더 큰 값으로 업데이트해준다.
6. 반복문을 모두 돌았음에도 true를 반환하지 못했다면 false를 반환한다.

### 시간 복잡도
O(n)

### 제출 코드
```javascript
var containsNearbyDuplicate = function(nums, k) {
  const obj = {};

  for (let i = 0; i < nums.length; i++) {
    if (nums[i] in obj && Math.abs(i - obj[nums[i]]) <= k) {
      return true;
    }
    obj[nums[i]] = i;
  }

  return false;
};
```

## Single Number
### 문제 풀이 01
1. `nums`를 순회하면서 각 숫자의 개수를 key - value 형태로 저장한다.
2. 개수가 홀수인 key를 반환한다.

### 시간 복잡도 01
O(n)

### 제출 코드 01
```javascript
var singleNumber = function(nums) {
  const hash = nums.reduce((acc, cur) => {
    acc[cur] ? acc[cur]++ : acc[cur] = 1;
    return acc;
  }, {});
  return Object.keys(hash).find((key) => hash[key] % 2);
};
```

### 문제 풀이 02
1. `nums`를 순회하면서 XOR 연산을 한다.  
   같은 비트를 가졌다면 XOR 연산을 했을 때 결괏값이 0이 나온다. 0과 0이 아닌 다른 숫자를 XOR 연산한다면 결괏값은 0이 아닌 다른 숫자가 나온다.
  ```
  2 ^ 2 = 0
  0 ^ 5 = 5
  ```
2. 최종 값을 반환한다.

### 시간 복잡도 02
O(n)

### 제출 코드 02
```javascript
var singleNumber = function(nums) {
  return nums.reduce((acc, cur) => acc ^ cur);
};
```

## Hamming Distance
### 문제 풀이 01
1. `x`와 `y`를 이진수로 변환 후 배열로 만든다.
```
1 = [1]
4 = [1, 0, 0]
```
2. 각 배열의 길이가 다르다면 반복문을 이용해 맨 앞에 0을 삽입한다.
```
1 = [0, 0, 1]
4 = [1, 0, 0]
```
3. 두 배열을 비교하며 반복문을 돈다. `i` 번째 값이 다를 경우 `count`를 1씩 올린다.

### 시간 복잡도 01
O(n)

### 제출 코드 01
```javascript
var hammingDistance = function(x, y) {
  const xArray = x.toString(2).split('').map(Number);
  const yArray = y.toString(2).split('').map(Number);
  
  const minLength = Math.min(xArray.length, yArray.length);
  const maxLength = Math.max(xArray.length, yArray.length);
  
  let count = 0;
  
  for (let i = minLength; i < maxLength; i++) {
    if (xArray.length < maxLength) {
      xArray.unshift(0);
    }
    
    if (yArray.length < maxLength) {
      yArray.unshift(0);
    }
  }
  
  for (let i = 0; i < maxLength; i++) {
    if (xArray[i] !== yArray[i]) {
      count += 1;
    }
  }
  
  return count;
};
```

### 문제 풀이 02
1. `x`와 `y`를 이용하여 XOR 연산을 한다.  
XOR 연산을 하는 이유는 두 이진수를 비교하여 같은 것은 0, 다른 것은 1로 표시하기 위해서다.
```
1 = 001
4 = 100
---------
    101
```
2. 연산한 값을 이진수로 변환한다.
```
101
```
3. 0은 비트가 같다는 의미이므로 `replace`를 이용하여 제거한다.
```
11
```
4. 해당 문자열의 길이를 반환한다.

### 시간 복잡도 02
O(n)

### 제출 코드 02
```javascript
var hammingDistance = function(x, y) {
  return (x ^ y).toString(2).replace(/0/g, '').length;
};
```
