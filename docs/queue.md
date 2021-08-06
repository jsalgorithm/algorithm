# 큐(Queue)

<img src="https://user-images.githubusercontent.com/33214449/127793558-63f0ac4b-3074-49c5-9f6f-5e2ee87ecb1b.png" width="700">

- FIFO(선입선출, First In First Out): 먼저 들어간 데이터가 먼저 나오는 자료구조
- 선형(linear) 자료구조
- ex) 자바스크립트 엔진에서 비동기 함수 실행시 콜백들이 대기열로 들어오는 `Task queue`

# 큐의 특징

## 큐의 메소드

- `enqueue`: 데이터를 삽입하는 연산
- `dequeue`: 데이터를 꺼내는 연산
- `length`: 큐에 있는 데이터의 수
- `peek`: 다음에 나올 데이터(큐에 가장 먼저 들어간 데이터)를 확인
- `isEmpty`: 현재 큐가 비어있는지 확인
- `clear`: 큐를 초기화

큐가 가득 차있으면 `enqueue`할 수 없고, 비어있으면 `dequeue`하거나 `peek` 할 수 없다.

## 큐의 속성

- front: 데이터를 꺼내는 쪽
- rear: 데이터를 넣는 쪽

# 큐 구현 방법

- 배열로 구현
- 배열로 순환큐를 만들어 구현(원형큐, 링버퍼)
- 연결리스트로 구현
- 스택 2개로 구현

# 배열로 간단하게 큐를 구현하기 (JavaScript)

- 자바스크립트의 `push()`, `shift()`를 사용

## pseudo code

## 전체 코드

```js
class Queue {
  constructor() {
    this.arr = [];
  }

  enqueue(data) {
    this.arr.push(data);
  }
  dequeue() {
    this.arr.shift();
  }
  length() {
    return this.arr.length;
  }
  peek() {
    return this.arr[0];
  }

  clear() {
    this.arr = [];
  }
  print() {
    console.log(this.arr);
  }
}

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(10);
queue.enqueue(100);
queue.print(); // [1,10,100]
queue.dequeue();
queue.print(); // [10,100]
console.log(queue.peek()); // 10
console.log(queue.length()); // 2
queue.clear();
queue.print(); // []
```

- 참고) `shift()`메소드의 경우 배열 맨 앞의 값을 삭제하고 배열의 기존 요소들을 앞으로 당겨줘야하므로 성능이 좋지 않다.

# References

- [JavaScript로 Stack 구현하기](https://gogomalibu.tistory.com/52)
- [자바스크립트로 스택과 큐 구현하기](https://velog.io/@raram2/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A1%9C-%EC%8A%A4%ED%83%9D%EA%B3%BC-%ED%81%90-%EA%B5%AC%ED%98%84%ED%95%98%EA%B8%B0-Stack-Queue)⭐
  - 연결리스트로 스택 구현, 2개의 스택으로 큐 구현
- [javascript로 queue 구현](https://jinchuu1391.tistory.com/48)
  - 우선순위 큐
