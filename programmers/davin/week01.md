# 1주차 알고리즘
## Valid Parentheses
### 문제 풀이
1. 문자열 `s`를 배열로 변환하여 반복문을 돈다.
2. 여는 괄호일 경우 무조건 `stack`에 `push` 한다.
3. 닫는 괄호일 경우 `stack`에 쌓인 마지막 괄호와 짝이 맞는지 검사한다.
4. 짝이 맞다면 `pop`을 이용하여 `stack`에서 제거한다.
5. 짝이 맞지 않다면 `stack`에 `push` 한다.

### 시간 복잡도
`s` 배열을 모두 순회해야 하므로 O(n)

### 제출 코드
```javascript
var isValid = function(s) {
	const stack = [];
	const bracket = {
		')': '(',
		'}': '{',
		']': '[',
	};

	s.split('').forEach((item) => {
		if (bracket[item]) {
			const lastItem = stack[stack.length - 1];
			lastItem === bracket[item] ? stack.pop() : stack.push(item);
		} else {
			stack.push(item);
		}
	});

	return !stack.length;
};
```

## Min Stack
### 문제 풀이
`this`를 이용하여 `MinStack` 함수의 인스턴스가 `stack`을 갖도록 선언한다.
- __push__ : `stack`의 마지막 인덱스에 값을 할당한다.
- __pop__ : `splice`를 이용하여 `stack`의 마지막 요소를 제거하고 그 값을 반환한다.
- __top__ : `stack`의 마지막 요소를 반환한다.
- __getMin__ : `Math.min`을 이용하여 `stack`의 최솟값을 반환한다. 

### 시간 복잡도
- __push__ : `stack`의 길이와 상관없이 무조건 마지막 인덱스에 값을 할당하므로 O(1)
- __pop__ : `stack`의 길이와 상관없이 무조건 마지막 요소를 제거하므로 O(1)
- __top__ : `stack`의 길이와 상관없이 무조건 마지막 요소를 반환하므로 O(1)
- __getMin__ : `stack`의 길이가 길어질수록 비교해야 하는 값이 늘어나기 때문에 O(n)

### 재출 코드
```javascript
var MinStack = function() {
	this.stack = [];
};

MinStack.prototype.push = function(val) {
	this.stack[this.stack.length] = val;
};

MinStack.prototype.pop = function() {
	return this.stack.splice(-1);
};

MinStack.prototype.top = function() {
	return this.stack[this.stack.length - 1];
};

MinStack.prototype.getMin = function() {
	return Math.min(...this.stack);
};
```

## Number of Recent Calls
### 문제 풀이
1. `this`를 이용하여 `RecentCounter` 함수의 인스턴스가 `queue`를 갖도록 선언한다.
2. `최근 호출 시간 - 3000` ~ `최근 호출 시간` 사이의 호출 횟수를 구해야 하므로 `최근 호출 시간 - 3000`을 구한다. (`ms`)
3. `queue`에 `t`를 `push` 한다.
4. `ms`가 0보다 작거나 같을 경우 처음부터 최근까지의 호출 횟수를 반환해야 하므로 `queue`의 `length`를 반환한다.
5. `ms`가 0보다 큰 경우 `for` 문을 돌면서 `ms` 이전에 호출된 값들은 `shift`를 이용하여 `queue`에서 제거한다.
6. `t`는 무조건 이전보다 더 큰 숫자를 받으므로 `ms`와 같거나 더 큰 경우 반복문을 멈춘다.

### 시간 복잡도
`queue`를 순회하면서 `ms`와 값을 비교해야 하므로 O(n)  
(특정 조건이면 `break`를 하지만 `queue`의 절반 이상을 검사하지 않는다는 보장이 없다고 생각해서 O(n)이라고 적었습니다.)

### 제출 코드
```javascript
var RecentCounter = function() {
	this.queue = [];
};

RecentCounter.prototype.ping = function(t) {
	const ms = t - 3000;
	this.queue.push(t);

	if (ms > 0) {
		for (let i = 0; i < this.queue.length; i++) {
			if (this.queue[i] < ms) {
				this.queue.shift();
				i--;
			} else {
				break;
			}
		}
	} 

	return this.queue.length;
};
```

## 프린터
### 문제 풀이
1. 숫자 배열이었던 `priorities`를 `map`을 이용하여 객체 배열(`queue`)로 만든다.
```javascript
[
	{ priority: 4, location: 0 },
	{ priority: 2, location: 1 },
	{ priority: 3, location: 2 },
	{ priority: 1, location: 3 },
	{ priority: 1, location: 4 },
]
```
2. `for` 문을 돌면서 `i` 번째의 `priority`와 그 이후 목록의 `priority`를 비교한다.
3. 이후 목록에 더 높은 `priority`가 있다면 `i` 번째 요소를 `splice`를 이용하여 잘라내고 `push`를 이용하여 맨 뒤로 넣는다.
4. 반복문을 끝까지 돌아 `priority` 순서대로 정렬되면, `findIndex`를 이용하여 `location`이 일치하는 요소의 인덱스를 구한다.
5. 인덱스 + 1을 반환한다.

### 시간 복잡도
`for` 문을 돌면서 `slice`, `find` 메서드를 사용하므로 시간 복잡도는 O(n2)

### 재출 코드
```javascript
function solution(priorities, location) {
	const queue = priorities.map((priority, index) => ({
		priority,
		location: index,
	}));

	for (let i = 0; i < queue.length; i++) {
		const currentItem = queue[i];
		const hasHigherPriority = !!queue
			.slice(i + 1)
			.find((item) => item.priority > currentItem.priority);

		if (hasHigherPriority) {
			queue.splice(i, 1);
			queue.push(currentItem);
			i--;
		}
	}

	const index = queue.findIndex((item) => item.location === location);
	return index + 1;
}
```
