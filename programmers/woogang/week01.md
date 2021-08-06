# 알고리즘 1주차

## Valid Parentheses

### 문제 설명

문자열에서 대괄호를 일치시키고 올바르게 닫혀있는지 확인하는 문제

### 문제풀이

push 메서드와 pop메서드를 사용

1. 각각 괄화로를 짝지어 object로 만든다.
2. 열린괄호면 stack에 넣는다
3. 닫힌 괄호는 전 값이 맞는 짝일 경우 stack에서 제거
4. 짝이 맞지 않을 경우 false를 반환
5.

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

### Min Stack
