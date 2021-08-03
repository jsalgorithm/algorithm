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

