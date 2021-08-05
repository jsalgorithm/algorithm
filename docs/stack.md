## What is stack?

스택은 자료구조 중에서도 데이터들이 일렬로 저장되어 있는 선형구조에 해당한다.  
대표적으로 프로그램을 수행할 때 사용된다.

![스택 참고자료](https://images.velog.io/images/solseye/post/4352d56e-f491-4e84-892a-1134761077ad/stack%20%E1%84%8E%E1%85%A1%E1%86%B7%E1%84%80%E1%85%A9.jpeg)

> 💡 [영상으로 구현된 스택](https://visualgo.net/ko/list)

### #1 stack의 특징

- LIFO(Last In First Out)
  스택에서는 데이터가 입력되는 순서대로 쌓이며, 나중에 들어온 데이터부터 먼저 사용된다. ex) 접시 쌓기
- 스택 메서드
  push(el) : 스택에 데이터를 삽입하는 연산  
  pop() : 스택에 있는 데이터를 삭제하는 연산  
  peek() : 스택에 가장 마지막으로 들어온 데이터 확인  
  isEmpty() : 스택이 비어있는지 확인  
  size() : 스택에 있는 데이터의 수 확인
- top
  가장 나중에 들어온 데이터의 위치
- 스택은 연결 리스트 방식과 리스트 방식 모두 이용하여 구현할 수 있으나, 연결 리스트 방식을 사용했을 때 추가, 삽입, 삭제 시 전체 데이터의 변동이 없어서 훨씬 속도가 빠르다.
- 스택이 가득 차 있으면 데이터를 삽입할 수 없다. => stack overflow
- 스택이 비어 있으면 데이터를 삭제할 수 없다. => stack underflow

### #2 JavaScript로 구현한 stack

```javascript
class Stack {
	constructor() {
		this._arr = [];
	}
	push(item) {
		this._arr.push(item);
	}
	pop() {
		return this._arr.pop();
	}
	peek() {
		return this._arr[this._arr.length - 1];
	}
}

const stack = new Stack();
stack.push(1);
stack.push(2);
stack.push(3);
stack.pop(); // 3
stack.peek(); // 2
stack.pop(); // 2
stack.peek(); // 1
```

### #3 stack의 활용 예시

- 작업 실행취소 ex) Ctrl+Z
- 웹 브라우저 방문기록 ex) 뒤로가기
- 프로그램에서 함수를 불러 수행할 때
- 컴퓨터에서 수식의 연산을 수행할 때 => 후위 표기법
- 재귀 호출 ex) 하노이의 탑
