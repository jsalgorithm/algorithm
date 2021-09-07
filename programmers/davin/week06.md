# 6주차 알고리즘
## Design Circular Deque
### 문제 풀이
- `MyCircularDeque`  
  생성자 함수에서 `deque`와 `maxSize`를 선언한다.
- `isEmpty`  
  `deque`의 length를 이용하여 배열이 비었는지 확인한다.
- `isFull`  
  `deque`의 length와 `maxSize`가 같은지 확인한다.
- `insertFront`  
  `isFull` 메서드를 이용하여 `deque`가 꽉 찼는지 확인한다.  
  만약 꽉 찼다면 `false`를 반환하고, 아니라면 `unshift` 메서드를 사용해서 값을 추가한 후 `true`를 반환한다.
- `insertLast`  
  `isFull` 메서드를 이용하여 `deque`가 꽉 찼는지 확인한다.  
  만약 꽉 찼다면 `false`를 반환하고, 아니라면 `push` 메서드를 사용해서 값을 추가한 후 `true`를 반환한다.
- `deleteFront`  
  `isEmpty` 메서드를 이용하여 `deque`가 비었는지 확인한다.  
  만약 비었다면 `false`을 반환하고, 아니라면 `shift` 메서드를 사용해서 값을 제거한 후 `true`를 반환한다.
- `deleteLast`  
  `isEmpty` 메서드를 이용하여 `deque`가 비었는지 확인한다.  
  만약 비었다면 `false`을 반환하고, 아니라면 `pop` 메서드를 사용해서 값을 제거한 후 `true`를 반환한다.
- `getFront`  
  `isEmpty` 메서드를 이용하여 `deque`가 비었는지 확인한다.  
  만약 비었다면 `-1`을 반환하고, 아니라면 `deque[0]`을 반환한다.
- `getRear`  
  `isEmpty` 메서드를 이용하여 `deque`가 비었는지 확인한다.  
  만약 비었다면 `-1`을 반환하고, 아니라면 `deque[deque.length - 1]`을 반환한다.

### 시간 복잡도
`deque`의 길이와 상관없이 모든 메서드는 O(1)의 시간 복잡도를 갖는다.

### 제출 코드
```javascript
var MyCircularDeque = function(k) {
  this.deque = [];
  this.maxSize = k;
};

MyCircularDeque.prototype.insertFront = function(value) {
  if (this.isFull()) {
    return false;
  }
  this.deque.unshift(value);
  return true;
};

MyCircularDeque.prototype.insertLast = function(value) {
  if (this.isFull()) {
    return false;
  }
  this.deque.push(value);
  return true;
};

MyCircularDeque.prototype.deleteFront = function() {
  if (this.isEmpty()) {
    return false;
  }
  this.deque.shift();
  return true;
};

MyCircularDeque.prototype.deleteLast = function() {
  if (this.isEmpty()) {
    return false;
  }
  this.deque.pop();
  return true;
};

MyCircularDeque.prototype.getFront = function() {
  if (this.isEmpty()) {
    return -1;
  }
  return this.deque[0];
};

MyCircularDeque.prototype.getRear = function() {
  if (this.isEmpty()) {
    return -1;
  }
  return this.deque[this.deque.length - 1];
};

MyCircularDeque.prototype.isEmpty = function() {
  return !this.deque.length;
};

MyCircularDeque.prototype.isFull = function() {
  return this.deque.length === this.maxSize;
};
```

## Design Circular Deque
### 문제 풀이
1. `values` 배열을 선언한다.
2. `lists` 반복문을 돌면서 노드의 값들을 모두 꺼내 `values`에 push 한다.
3. `values`의 length가 0이면 `null`을 반환한다. (노드를 만들 수 없으므로)
4. `values`를 오름차순으로 정렬한다.
5. `values`의 첫 번째 요소로 `head`를 만든 후, 노드를 만들기 위해 `temp`를 선언하여 `head`를 할당한다.
6. `values` 반복문을 돌면서 `head`의 `next`에 새로운 노드들을 이어준다.
7. `head`를 반환한다.

### 시간 복잡도
O(n)

### 제출 코드
```javascript
var mergeKLists = function(lists) {
  const values = [];
  
  for (let i = 0; i < lists.length; i++) {
    let currentNode = lists[i];
    
    while (currentNode) {
      if (currentNode) {
        values.push(currentNode.val);
        currentNode = currentNode.next;
      }
    }
  }
  
  if (values.length === 0) {
    return null;
  }
  
  values.sort((a, b) => a - b);
  
  const head = new ListNode(values[0]);
  let temp = head;
  
  for (let i = 1; i < values.length; i++) {
    temp.next = new ListNode(values[i]);
    temp = temp.next;
  }
  
  return head;
};
```
