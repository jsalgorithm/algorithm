## 스택(Stack) 1번 문제

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

-- 방법 2

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
