# 3주차 알고리즘
## 정렬문제
### K번째 수

### 코드

```javascript
function solution(array, commands) {
  const answer = [];
    
    commands.forEach(command => {
        const arrayCommand = array.slice(command[0]-1, command[1]);
        arrayCommand.sort((a,b) => a - b);
        answer.push(arrayCommand[command[2]-1]);
    })
    return answer;
}
```

### 풀이방법

Array.silce()이용해서 풀이

1.  arrayCommand: slice() 메서드를 이용해  array에서 필요한 부분을 자른다.
2.  잘라낸 배열을 arrayCommand를 오름차순으로 정렬
3.  정렬한 배열에서 K번째 수를 answer에 push
4.  forEach무이 완료되면 answer를 return함.


***

## 완전탐색
### 모의고사
### 코드

```javascript
function solution(answers) {
​
    let answer = [];
    let supo = [
        [1, 2, 3, 4, 5],
        [2, 1, 2, 3, 2, 4, 2, 5],
        [3, 3, 1, 1, 2, 2, 4, 4, 5, 5],
    ];
​
    let score = [];
    for (let i = 0; i < supo.length; i++) {
        let result = 0;
​
        for (let j = 0; j < answers.length; j++) {
            supoAnswers = supo[i][j % supo[i].length];
​
            if (answers[j] === supoAnswers) {
                result++;
            }
        }
        score.push(result);
    }
​
    for (let i = 0; i < score.length; i++) {
        if (score[i] === Math.max(...score)) {
            answer.push(i + 1);
        }
    }
​
    return answer;
}
```
​
### 문제풀이
​
1.  수포자가 찍는 방식을 배열로 만든다 >> 수포자의 수 만큼 for문을 돌린다
2.  인덱스의 값(예시>>\[1,2,3,4,5\])이 반복 되므로 5로 나눈 인덱스 값을 sudoAnwers에 넣고 정답과 비교하면 result 값을 구한다
3.  수포자들의 맞는 개수를 score 배열에 넣고 최고점과 같을 경우  answer에 넣는다
4.  answer을 반환(return)한다



