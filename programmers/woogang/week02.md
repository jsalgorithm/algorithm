# 2주차 알고리즘
# hash 문제
## 완주하지 못한 선수
### 문제풀이

1\. 참가자와 완주자 배열을 정렬해준다

2\. 참가자.가 끝날 때까지 반복

3.만약 참가자와 완주자가 맞지않는다면 비완주자를 리턴한다.

//참가자 배열 정리

//완주자 배열 정리

//참가자가 끝날때까지 반복

//만약 참가자와 완주자가 맞지않으면

//참가자목록(==비완주자) 반환

#### 코드

```
function solution(participant, completion) {
    participant.sort(); //참가자 배열 정렬
    completion.sort(); //완주자 배열 정렬
    for(var i=0;i<participant.length;i++){
        if(participant[i] !== completion[i]){
            //인덱스 0부터 순차적으로 두 배열 비교
            return participant[i];
            //비완주자가 참가자 배열에 나올 경우 출력
        }
    }
}
```
***
## 위장
#### 코드

```
function solution(clothes) { 
    var answer = 1; 
    var obj = {};
    
    for(var i=0; i<clothes.length; i++){
        if(obj[clothes[i][1]] >= 1){
            obj[clothes[i][1]] += 1; //객체에 이미 같은 키값이 있다면 +1을 해준다.
        } else{
            obj[clothes[i][1]] = 1;// 새로운 종류의 옷(키 값)이라면 1로 만든다.
        }
    }
        for(var key in obj){
            answer *= (obj[key]+1);//각 옷 종류마다 안입는 경우를 포함
        }
        return answer -1; //전체 경우의 수에서 모두 안입는 경우 제외
    }
```

### 문제풀이

-   빈객체(obj) 생성
-   각 옷종류마다 안입는 경우가 있어서 +1씩 한 값들을 곱해준다 => 모든경우의 수가 만들어짐
-   answer -1을 하는 이유 : 문제에서 옷을 무조건 하나는 입고 있다고 함, 모든 경우의 수에서 아무것도 입지않는 경우의 수 1을 빼준다.

***

# 이분탐색 문제
##  Intersection of Two Arrays II
### 문제풀이
### 코드


## Find the Duplicate Number



