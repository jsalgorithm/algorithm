# 3주차 js 알고리즘

## 정렬 1번
[k번째수](https://programmers.co.kr/learn/courses/30/lessons/42748)

``` javascript
function solution(array, commands) {
    let answer = [];
    
    
    for(let i in commands)
        answer.push(array.slice(commands[i][0] - 1, commands[i][1]).sort((a, b) => a - b)[commands[i][2] - 1]);

    return answer;
}
```

## 정렬 2번
[가장 큰 수](https://programmers.co.kr/learn/courses/30/lessons/42746)

```javascript
 function solution(numbers) {
    var answer = numbers.map(c=> c + '').
    				sort((a,b) => (b+a) - (a+b)).join('');
    
    return answer[0]==='0'? '0' : answer;
}
```

---


## 완전탐색 1번
[모의고사](https://programmers.co.kr/learn/courses/30/lessons/42840)

```javascript
function solution(answers) {
    // students: 수포자 답안 패턴
    const students = [
        [ 1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]
    ];
    // score: 수포자들의 점수
    let score = [];
    
    for(let student of students){
        score.push(answers.reduce((acc,curr,idx) => {
            // 해당 idx정답이 수포자의 정답 패턴에 일치할 경우, 점수증가
            curr === student[idx%student.length] ? acc++ :acc;
            // 해당 수포자의 점수를 score배열에 push
            
            return acc;
        },0));
    }
    
    // 가장 많은 문제를 맞힌 사람 return
    return score.reduce((acc,curr,idx) => {
        // 현재 수포자의 점수가 최대 점수와 같을 경우, idx+1 값을 배열에 push
        
        curr === Math.max(...score) ? acc.push(idx+1) : acc;
        return acc;
    },[]);
}

```
## 완전탐색 2번
[소수찾기](https://programmers.co.kr/learn/courses/30/lessons/42839)

```javascript
function solution(numbers) {
    const stack = [];
    
    // bfs를 이용해 만들 수 있는 모든 숫자 찾기
    const prime = (num) => {
        const sqrt = Math.floor(Math.sqrt(num));
        
        for (let i = 2; i <= sqrt; i += 1) {
            if (num % i === 0) {
                return false;
            }
        }
        return true;
    }
    
    const makeANum = (num, idx) => {
        if (num.length === numbers.length) return;
        
        for (let i = 0; i < numbers.length; i += 1) {
            if (idx.indexOf(i) !== -1) continue;
            
            const newNum = num + numbers[i];
            
            if (stack.indexOf(parseInt(newNum)) === -1 && parseInt(newNum) >= 2) {
                const isPrime = prime(parseInt(newNum));
                
                if (isPrime) {
                    stack.push(parseInt(newNum));
                }
            }
            makeANum(newNum, [...idx, i]);
        }
    }
    
    makeANum('', []);
    
    return stack.length;
}

```