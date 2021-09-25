# 알고리즘 1주차

## Valid Parentheses
### 문제풀이
문자열에서 대괄호를 일치시키고 올바르게 닫혀있는지 확인하는 문제

push 메서드와 pop메서드를 사용

1. 각각 괄화로를 짝지어 object로 만든다.
2. 열린괄호면 stack에 넣는다
3. 닫힌 괄호는 전 값이 맞는 짝일 경우 stack에서 제거
4. 짝이 맞지 않을 경우 false를 반환


```
var isValid = function(s) {
     const temp = {
        '(' : ')',
        '{' : '}',
        '[' : ']'
    };
    const stack = [];
    const keys = Object.keys(temp);
        for(let i = 0; i<s.length; i++) {
            if(keys.includes(s[i])) {
                stack.push(s[i]);
            }
        else {
            if (temp[stack[stack.length-1]] === s[i]) {
                stack.pop();
            }
        else{
            return false;
            }
          }
        };
    return !stack.length;

};
```
***
### Min Stack

### 문제풀이
스택을 사용해서 min stack을 구현하는 문제
1. 들어온 순서대로 쌓아 올리는 스택
2. 대응하여 현재까지 최소값을 저장하는 스택으로 사용
### 코드
```
/**
 * initialize your data structure here.
 */
var MinStack = function () {
  this.stack = [];
  this.minStack = [];
  this.minValue = Infinity;
};

/**
 * @param {number} x
 * @return {void}
 */
MinStack.prototype.push = function (x) {
  this.stack.push(x);
  this.minValue = Math.min(this.minValue, x);
  this.minStack.push(this.minValue);
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
  this.stack.pop();
  this.minStack.pop();

  if (this.minStack.length > 0) {
    this.minValue = this.minStack[this.minStack.length - 1];
  } else {
    this.minValue = Infinity;
  }
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
  return this.minValue;
};
```

***
## Number of Recent Calls

### 문제풀이
Array Queue를 이용해 3000 ms이전의 값은 모두 삭제하고 남아있는 length를 리턴

### 코드
```
var RecentCounter = function() {
    this.queue = new Array();
};

RecentCounter.prototype.ping = function(t) {
    
    if(0 < this.queue.length){
        while(3000 < t - this.queue[0]){
            this.queue.shift();
        }
    }
    
    this.queue.push(t);
    
    return this.queue.length;
};
```

+ 참고블로그 : https://enumclass.tistory.com/91

***
## 프린트

### 코드
```
function solution(priorities, location) {
    var list = priorities.map((t,i)=>({
        my : i === location,
        val : t
    }));
    var count = 0;        
    while(true){
        var cur = list.splice(0,1)[0];        
        if(list.some(t=> t.val > cur.val )){
            list.push(cur);                        
        }
        else{            
            count++;
            if(cur.my) return count;
        }
    }
}
```

+ 참고 블로그: https://greedysiru.tistory.com/561




