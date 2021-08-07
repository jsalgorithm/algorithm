# week 01 

## Valid parentheses

```
const isValid = function (s) {
	if (s.length % 2 !== 0) return false;
	const pairs = {
		"{": "}",
		"[": "]",
		"(": ")",
	};
	let stack = [];
	for (let i = 0; i < s.length; i++) {
		if (pairs.hasOwnProperty([s[i]])) {
			stack.push(s[i]);
			continue;
		}
		if (pairs[stack[stack.length - 1]] === s[i]) {
			stack.pop();
			continue;
		}
		return false;
	}
	console.log(stack.length);
	if (stack.length === 0) return true;
	return false;
};
```

## sudo code

```
const isValid = function (s) {
	if(주어진 s의 길이가 짝수가 아니라면) return false;
	const pairs = {
		"{": "}",
		"[": "]",
		"(": ")",
	}; 
	let stack = [];
	
	for(s의 길이만큼 반복문 실행){
		if(s[i]의 값이 pairs의 key값이라면){
			stack.push(s[i])
			continue
		};
		if(pairs[stack의 마지막 값] 가 s[i]와 같다면){
			stack.pop()
			continue;
		}
		아니라면 return false
	}
	반복문이 종료되면,
	if(stack.length === 0) return true;
	return false;
}
```

### 시간복잡도

위 문제에서 시간복잡도는 O(n)이다. 문제를 풀기 위해 주어진 string을 전부 탐색해야하기 때문이다.

` s = " ()] " ` 인 경우,  마지막 요소인 ]는 택도 없지만, true, false를 확인하기 위해 주어진 s의 모든 요소를 탐색해야한다.

## MinStack

```
var MinStack = function () {
	this.stack = [];
};

MinStack.prototype.push = function (val) {
	this.stack.push(val);
};


MinStack.prototype.pop = function () {
	return this.stack.pop();
};


MinStack.prototype.top = function () {
	return this.stack[this.stack.length - 1];
};


MinStack.prototype.getMin = function () {
	return this.stack.reduce((a, b) => (a > b ? b : a));
};

```

### 시간복잡도

stack에서 pop, push, top 모두 O(1)의 시간 복잡도를 가진다.\n

데이터 맨 위나 아래에서 데이터를 가져오기 때문이다.

getMin의 경우 스택 내의 모든 수를 탐색하며 최소값을 찾아야하므로 O(n)의 시간복잡도를 가진다.

## recentCounter

```
var RecentCounter = function () {
	this.queue = [];
};


RecentCounter.prototype.ping = function (t) {
	this.queue.push(t);
	while (this.queue[0] < t - 3000) {
		this.queue.shift();
	}
	return this.queue.length;
};

```

## 시간복잡도

queue에서 push의 경우 데이터의 맨 아랫쪽에 삽입하기 때문에, O(1)의 시간복잡도를 가진다.

## 프린터

```
// 인쇄되는 조건과 내 문서의 위치, 인쇄가 몇 번 됐는지 체크
function solution(priorities, location) {
	let answer = 0;
	while (priorities.length) {
		let current = priorities[0];
		if (current < Math.max(...priorities)) {
			if (location === 0) {
				location = priorities.length;
			}
			priorities.shift();
			priorities.push(current);
		} else {
			answer++;
			if (location === 0) {
				break;
			}
			priorities.shift();
		}
		--location;
	}
	return answer;
}

console.log(solution([1, 1, 9, 1, 1, 1], 0));
```

## 시간복잡도

location에 해당하는 문서가 출력이 될 때 까지 탐색을 반복하므로 O(n)의 시간복잡도를 갖게된다.
