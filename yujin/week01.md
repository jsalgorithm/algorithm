# 1주차 js 알고리즘

## stack 1번
[valid-parentheses](https://leetcode.com/problems/valid-parentheses/)

``` javascript
/**
 * @param {string} s
 * @return {boolean}
 */

var isValid = function(s){
    const temp = {
        '(':')',
        '[':']',
        '{':'}'
    };
    const stack = [];
    const keys = Object.keys(temp);
    for (let i = 0; i<s.length; i++) {
        if (keys.includes(s[i])){
            stack.push(s[i]);
        }else {
            if (temp[stack[stack.length-1]] === s[i]) {
                stack.pop();
            }else {
                return false;
            }
        }
    };
    return !stack.length;
}
```

## stack 2번
[Min Stack](https://leetcode.com/problems/min-stack/)

```javascript
 */
var MinStack = function() {
    this.st = [];
};

/** 
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function(val) {
    this.st[this.st.length] = val;
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    return this.st.splice(-1);
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    return this.st[this.st.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
    return Math.min(...this.st);
};
```

---


## queue 1번
[Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/)

```javascript


```