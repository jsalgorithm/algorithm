# 5주차 알고리즘
## Two Sum
### 문제 풀이
1. `result` 배열과 `nums`를 복사한 `copy`를 선언한다.
2. `for` 문을 이용하여 `nums`를 순회한다.
3. 현재의 숫자 `current`를 선언하고, `copy` 배열에서 해당 숫자를 `null`로 만든다.
```javascript
nums = [2, 3, 4]
current = 2
copy = [null, 3, 4]
```
4. `findIndex`를 이용해서 `num` + `current` === `target`이 되는 인덱스를 찾는다.
5. 해당 인덱스가 존재하면 `result`에 `push` 하고 반복문을 종료한다.
6. 만약 존재하지 않는다면 `null`이 들어있는 `copy` 배열을 다시 원상복구 해준다.
7. 최종적으로 `result`를 리턴한다.

### 시간 복잡도
반복문 안에서 `findIndex` 메서드를 사용하고 있으므로 O(n^2)

### 제출 코드
```javascript
var twoSum = function(nums, target) {
  const result = [];
  let copy = [...nums];
  
  for (let i = 0; i < nums.length; i++) {
    const current = copy[i];
    copy[i] = null;
    const index = copy.findIndex((num) => typeof num === 'number' && num + current === target);

    if (index >= 0) {
      result.push(i, index);
      break;
    }
    
    copy = [...nums];
  }
  
  return result;
};
```
