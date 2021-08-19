# 알고리즘 1주차

- 주제: 스택(Stack), 큐(Queue)
- 작성자: 박유림(Wol-dan) / @pul8219

## 목차

- 스택
  - 문제 1) [Valide Parentheses](#valid-parentheses)
  - 문제 2) [Min Stack](#min-stack)
- 큐
  - 문제 1) [Number of Recent Calls](#number-of-recent-calls)
  - 문제 2) [프린터](#프린터)

# Valid Parentheses

- 문제 분류: `스택`
- 문제 출처: [LeetCode - 20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
- 라벨: `Easy`, `JavaScript`

## 문제

- 소괄호, 중괄호, 대괄호가 포함되어있는 문자열 `s`가 유효한지 검사하는 문제
- 열린 괄호와 닫힌 괄호의 짝이 맞도록 해야하고 옳은 순서로 괄호가 작성된 것만 `true`를 리턴해야한다. 자세한 예시는 문제의 Example에 나와있다.

![image](https://user-images.githubusercontent.com/33214449/128459996-e860d3b4-480d-4f7a-94ce-d18364413857.png)

## 풀이 과정

- 스택에 열림괄호에 대응하는 닫힘괄호를 push해서 이를 pop하며 확인하는 방식으로 구현했다.

- pseudo code

  ```
  var isValid = function (s) {
  const arr = [];

  const brackets = {
    '(': ')',
    '{': '}',
    '[': ']',
  };


  문자열을 돌며 반복{
      ✔️(if문) 현재 문자가 스택의 top에 저장된 열림괄호에 대응하는 닫힘괄호와 같다면{
          배열에서 top 요소를 꺼낸다(pop)
          (*** 스택이 비어있는 경우는 여기에 들어오지도 않고 else문으로 갈 것이다.)
      }
      ✔️(else문){ // 아래 if문으로 인해 스택에는 열림괄호만 들어갈 것이고 상단 if문이 아닌 이 곳 else문으로 왔다는 건 현재 문자가 스택 최상단요소에 대응하는 닫힘괄호가 아니라는 뜻이다.
          ✔️(if문) 현재문자가 ), }, ] 셋 중 하나이면 false를 리턴(invalid하니까 더이상 볼 필요가 없다는 것)
          위의 if문에도 해당되지 않으면 현재 문자를 스택에 넣기(push)
      }
  }

  끝까지 다 돌았으니 스택이 비어있으면 true를, 그렇지 않으면 false를 리턴하기
  ```

## 제출 코드

- 시간 복잡도: O(n)

```js
/**
 * 문제: LeetCode - 20. Valid Parentheses
 */
var isValid = function (s) {
  const arr = [];

  const brackets = {
    '(': ')',
    '{': '}',
    '[': ']',
  };

  for (elem of s) {
    if (brackets[arr[arr.length - 1]] === elem) arr.pop();
    else {
      if (elem === ')' || elem === ']' || elem === '}') return false;
      arr.push(elem);
    }
  }
  return arr.length === 0;
};
```

# Min Stack

- 문제 분류: `스택`
- 문제 출처: [LeetCode - 155. Min Stack](https://leetcode.com/problems/min-stack/)
- 라벨: `Easy`, `JavaScript`

## 문제

- `push`, `pop`, `top`를 지원하고, 상수시간에 가장 작은 값을 탐색할 수 있는 스택을 구현하라.
- `pop`, `top`, `getMin`은 스택이 비어있지 않을 때 호출된다.

---

- `MinStack()`: 스택을 초기화
- `void push(val)`: `val`를 스택에 push
- `void pop()`: 스택의 top에 있는 요소를 제거
- `int top()`: 스택의 top에 있는 요소를 반환
- `int getMin()`: 스택에서 가장 작은 요소를 검색

## 풀이 과정

- 데이터를 저장하는 `stack`, 최소값을 저장하는 `minstack` 이렇게 스택 2개를 써서 구현했다.
- push()와 pop()을 사용했다.
- push
  - 스택이 비어있을 땐 인자를 `stack`, `minstack` 모두에 푸시한다.
  - 푸시하려는 데이터가 스택의 현재 최소값(`minstack`의 `top`에 있는 요소)보다 작을 경우 해당 값을 `minstack`에 푸시하고, 아니라면 스택의 현재 최소값(`this.minstack[this.minstack.length - 1]`을 `minstack`에 한번 더 푸시한다.
- getMin() 메소드가 상수 시간(`O(1)`)에 실행되도록 작성했다.

## 제출 코드

- 시간 복잡도: getMin() 메소드의 경우 O(1)

```js
/**
 * 문제: LeetCode - 155. Min Stack
 * 시간 복잡도: getMin() 메소드의 경우 O(1)
 */

/**
 * initialize your data structure here.
 */
var MinStack = function () {
  this.stack = [];
  this.minstack = [];
};

/**
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function (val) {
  if (this.stack.length === 0) {
    this.stack.push(val);
    this.minstack.push(val);
    return;
  }

  if (val < this.minstack[this.minstack.length - 1]) this.minstack.push(val);
  else {
    this.minstack.push(this.minstack[this.minstack.length - 1]);
  }

  this.stack.push(val);
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
  this.stack.pop();
  this.minstack.pop();
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
  return this.minstack[this.minstack.length - 1];
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

# Number of Recent Calls

- 문제 분류: `큐`
- 문제 출처: [LeetCode - 944. Number of Recent Calls](https://leetcode.com/problems/number-of-recent-calls/)
- 라벨: `Easy`, `JavaScript`

## 문제

- `RecentCounter` class: 특정 time frame 이내에 들어온 요청의 개수를 세는 class
- `ping` 메소드: `t`(밀리초)시간에 들어온 요청을 추가한다. 요청들 중에 `t`시간으로부터 3000ms 내에 있는 요청들을 카운트하여 카운트된 개수를 반환하는 메소드이다. (`t-3000 이상, t 이하`)
- 이 문제에서는 `ping`의 인수로 전달되는 `t`는 점점 커지는 값임이 보장되어있다.

## 풀이 과정

처음에는 요청이 저장된 배열을 돌면서 각 요소마다 `t-3000 이상, t 이하` 조건을 검사해야하나 생각했다. 하지만 t가 점점 커지는 값만 들어온다는 게 보장되어있었기 때문에 그럴 필요가 없었다. 큐 개념을 이용해 들어오는 요청을 배열의 끝에 삽입하고, 조건을 검사할 땐 맨 앞의 요소만 검사해 조건에 맞지 않을 경우 큐배열에서 꺼냈다. 조건도 `t 이하`임은 확인할 필요가 없다. `ping` 호출시 들어온 요청 이전의 요청들은 현재 요청보다 t가 무조건 작기 때문이다. 따라서 큐배열의 `[0]`자리 요소가 `t-3000 이상`인지만 확인하면 된다.

- `RecentCounter`함수의 인스턴스가 `queue`를 갖도록 선언한다.
- `ping`이 호출되면 `queue`에 `t`를 `push`한다.
- `queue`의 첫번째 요소가 `최근호출t-3000`보다 작으면 `queue`에서 제거한다. 이 과정을 반복하다가 `최근호출t-3000`와 같거나 큰 경우 while문을 빠져나간다.
- `queue`의 `length`를 반환한다.(얻고자 하는 값)

> **splice vs shift**
>
> splice는 주어진 index에 위치한 요소를 삭제한 후 다른 요소들을 당긴 후 이렇게 변경된 배열을 리턴한다. (index에 위치한 요소를 찾아야하고 마지막에 배열의 모든 값을 참고해 새로운 배열을 리턴해야하니 할 작업이 많은 것 같다.)
>
> shift는 맨 첫번째 요소를 삭제한 후 뒤의 요소들을 앞으로 당기고 삭제한 요소만 리턴한다. shift가 splice보다 좀 더 빠른 것 같다.

## 제출 코드

- 시간 복잡도: 최악의 경우 ping을 호출한 개수만큼 반복하기 때문에 O(n) 예상

```js
/**
 * 문제: Leetcode - 944. Number of Recent Calls
 */

var RecentCounter = function () {
  this.queue = [];
};

/**
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function (t) {
  this.queue.push(t);
  while (this.queue[0] < t - 3000) {
    this.queue.splice(0, 1);
  }

  return this.queue.length;
};

/**
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```

# 프린터

- 문제 분류: `스택/큐`
- 문제 출처: [프로그래머스 level02. 프린터](https://programmers.co.kr/learn/courses/30/lessons/42587)
- 라벨: `Level 2`, `JavaScript`

## 문제

- `priorities` 배열의 처음부터 보면서 해당 문서보다 중요도가 높은 문서가 한 개라도 존재하면 해당 문서를 대기 목록의 가장 뒤로 보내고, 그렇지 않을 경우 해당 문서를 인쇄하는 문제이다.
- `priorities` 배열에서 `location`위치(배열 index 처럼 0부터 시작)에 있는 문서가 몇 번째로 인쇄되는지 반환하는 것이 목표이다.
- `priorities` 배열(=인쇄 대기 목록)의 값은 중요도를 나타낸다.

## 풀이 1

- `priorities` 배열을 큐로 보고 풀었다. 인쇄 순서가 밀리는 요소를 뒤에 넣는 대신 `front`, `rear` 변수를 갱신하며 큐의 처음과 끝을 나타내도록 하여 원형큐처럼 구현했다.
- 인쇄되는 문서는 `priorities` 배열에서 삭제하도록 했는데 이렇게 `priorities` 배열이 변경되니 `location`값을 어떻게 기억해야할지 고민됐다. 그래서 인쇄로 배열이 변경될 경우 `front`가 `location`보다 작다면(`location`이 당겨져야 하기 때문에) `location` 값이 1만큼 감소하도록 했다.
- 코드가 복잡한 것 같아서 더 간단하게 구현하고 싶다.

### 제출 코드

- 시간 복잡도: O(n^2)

```js
/**
 * 문제: 프로그래머스 - Level 2 프린터
 */

function solution(priorities, location) {
  var answer = 0;

  const max = priorities.length;
  let front = 0,
    rear = priorities.length - 1;

  /* 초기 pri 배열 요소 개수만큼 반복 */
  outer: for (let i = 0; i < max; i++) {
    inner: for (let j = 0; j < priorities.length; j++) {
      /* 현재 pri 배열에서 중요도가 가장 큰 수 저장 */
      // const max_pri = priorities.reduce(function (pre, val) {
      //   return Math.max(pre, val);
      // });
      const max_pri = Math.max(...priorities);

      /* 현재 문서보다 중요도가 높은 문서가 한 개라도 존재하면 */
      if (priorities[front] < max_pri) {
        // front, rear 변경 // 배열 길이 고려해 나머지 연산
        front = (front + 1) % priorities.length;
        rear = (rear + 1) % priorities.length;
      } else if (priorities[front] >= max_pri) {
        /* 중요도가 같거나 크면 인쇄 */
        priorities.splice(front, 1); // 인쇄 // priorities 배열에서 삭제
        answer++; // 인쇄된 문서 수 // 최종적으로는 인쇄를 요청한 문서가 몇번째로 인쇄되는지를 나타낼 것임
        if (front == location) break outer;
        // 현재 인쇄하려는 문서가 요청한 문서일 경우 가장 바깥 for문 종료(여기서 끝낸다는 것)
        else if (front < location) location--; // 배열이 변경되어 location index값에 영향을 줄 경우 location 값 변경

        /* front, rear값이 배열의 크기 이상인 경우 나머지 연산을 이용해 알맞게 가리키도록 함 */
        if (front >= priorities.length) front = front % priorities.length;
        if (rear >= priorities.length) rear = rear % priorities.length;
        break; // inner for문 반복을 종료하고 다음 반복으로 넘어감
      }
    }
  }

  return answer;
}
```

## 풀이 2

- [풀이 1](#풀이-1)과 동작은 비슷하나 `queue`에 location값도 저장해 코드를 풀이 1보다 간결하게 수정했다.

### 제출 코드

```js
/**
 * 문제: 프로그래머스 - Level 2 프린터
 */
function solution(priorities, location) {
  var answer = 0;

  const queue = priorities.map((priority, index) => ({
    priority,
    location: index,
  }));

  while (true) {
    const curItem = queue[0];
    const max_pri = queue.reduce(function (pre, val) {
      return pre.priority > val.priority ? pre : val;
    }).priority;

    if (queue[0].priority >= max_pri) {
      queue.splice(0, 1);
      answer++;
      if (curItem.location === location) break;
    } else {
      queue.splice(0, 1);
      queue.push(curItem);
    }
  }

  return answer;
}
```

## References

- [자바스크립트의 유용한 배열 메소드 사용하기 map(), filter(), find(), reduce()](https://bblog.tistory.com/300)
- [JavaScript 중첩 반복문에서 break, continue](https://graykick.tistory.com/4)
