## 스택(Stack) 1번 문제

**LeetCode | Valid Parentheses**

[문제 링크](https://leetcode.com/problems/valid-parentheses/)

### 코드

- 방법 1

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
	let stack = [];

	for (let i = 0; i < s.length; i++) {
		let lastStr = stack[stack.length - 1];
		if (s[i] === "(" || s[i] === "{" || s[i] === "[") stack.push(s[i]);
		else if (
			(lastStr === "(" && s[i] === ")") ||
			(lastStr === "{" && s[i] === "}") ||
			(lastStr === "[" && s[i] === "]")
		)
			stack.pop();
		else return false;
	}
	return stack.length === 0;
};
```

- 방법 2

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
	const brackets = { ")": "(", "}": "{", "]": "[" };
	let stack = [];

	for (let i = 0; i < s.length; i++) {
		if (s[i] === "(" || s[i] === "{" || s[i] === "[") stack.push(s[i]);
		else if (stack[stack.length - 1] === brackets[s[i]]) stack.pop();
		else return false;
	}
	return stack.length === 0;
};
```

---

## 스택(Stack) 2번 문제

**LeetCode | Min Stack**

[문제 링크](https://leetcode.com/problems/min-stack/)

### 코드

```javascript
var MinStack = function () {
	this.stack = [];
};

/**
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function (val) {
	return this.stack.push(val);
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
	if (this.stack == null) {
		return false;
	}
	return this.stack.pop();
};

/**
 * @return {number}
 */
MinStack.prototype.top = function () {
	return this.stack[this.stack.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function () {
	return Math.min.apply(null, this.stack);
};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```

---

## 큐(queue) 1번 문제

**LeetCode | Number of Recent Calls**

[문제 링크](https://leetcode.com/problems/number-of-recent-calls/)

### 코드

- 방법 1

```javascript
var RecentCounter = function () {
	this.queue = [];
};

/**
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function (t) {
	if (this.queue === null) return null;
	this.queue.push(t);
	let min = t - 3000;
	let max = t;
	let result = [];
	for (const n of this.queue) {
		if (n >= min && n <= max) result.push(n);
	}
	return result.length;
};

/**
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```

- 방법 2

```javascript
class RecentCounter {
	constructor() {
		this.queue = [];
	}

	ping(t) {
		this.queue.push(t);
		while (this.queue[0] < t - 3000) {
			this.queue.shift();
		}

		return this.queue.length;
	}
}
```

---

## 큐(queue) 2번 문제

**Programmers | 프린터**

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42587)

### 코드

```javascript
function solution(priorities, location) {
	let answer = 0;
	let point = location;

	while (true) {
		let curDoc = priorities.shift();
		if (priorities.some((e) => e > curDoc)) priorities.push(curDoc);
		else {
			answer++;
			if (point === 0) return answer;
		}

		point--;
		if (point === -1) {
			point = priorities.length - 1;
		}
	}
	return answer;
}
```
