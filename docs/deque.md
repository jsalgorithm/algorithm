# 데크(Deque)

![image](https://user-images.githubusercontent.com/33214449/132878454-d6754ba3-d897-46cd-9711-b3d4561f1bab.png)

출처: <https://soft.plusblog.co.kr/24>

데크(Deque)는 Double ended Queue의 약자로 양쪽에서 입력, 출력이 모두 가능한 자료구조이다. 큐와 스택을 합친 개념으로도 생각할 수 있다.

## 데크의 종류

데크에 제약조건을 주어 목적에 따라 다르게 데크를 사용할 수 있다.

- 스크롤(Scroll): 입력이 한쪽에서만 가능하고 출력은 양쪽 모두에서 가능한 데크
- 셸프(Shelf): 출력이 한쪽에서만 가능하고 입력은 양쪽 모두에서 가능한 데크

## 데크 구현 in JavaScript

이중 연결 리스트(Doubly Linked List)를 이용한 데크 구현

> 이중 연결 리스트(Doubly Linked List)는 노드에 2개의 링크가 존재하여 노드가 자신의 이전 노드와 다음 노드를 알고 있는 자료구조를 의미한다.

```js
class Node {
  constructor(value) {
    this.value = value ? value : null;
    this.next = null;
    this.prev = null;
  }
}
class Deque {
  constructor() {
    this.head = null;
    this.tail = null;
    this.count = 0;
  }

  pushFront(elem) {
    if (this.head === null) {
      this.head = elem;
      this.tail = elem;
    } else {
      let cur = this.head;
      elem.next = cur;
      cur.prev = elem;
      this.head = elem;
    }
    this.count++;
  }

  popFront() {
    if (!this.isEmpty()) {
      let temp = this.head;
      temp.next.prev = null;
      this.head = temp.next;
      temp = null;
      this.count--;
    }
  }

  pushBack(elem) {
    if (this.tail === null) {
      this.head = elem;
      this.tail = elem;
    } else {
      this.tail.next = elem;
      elem.prev = this.tail;
      this.tail = elem;
    }
    this.count++;
  }

  popBack() {
    if (!this.isEmpty()) {
      let temp = this.tail;
      temp.prev.next = null;
      this.tail = temp.prev;
      temp = null;
      this.count--;
    }
  }

  peekFront() {
    return this.head.value;
  }

  peekBack() {
    return this.tail.value;
  }

  isEmpty() {
    if (!this.count) return true;
    else return false;
  }

  print() {
    let cur = this.head;
    while (cur) {
      console.log(cur.value);
      cur = cur.next;
    }
  }

  length() {
    return this.count;
  }
}

const deque = new Deque();
deque.pushFront(new Node(1));
deque.pushFront(new Node(2));
deque.pushBack(new Node(3));
deque.pushBack(new Node(4));

deque.print(); // 2-1-3-4
console.log(`head: ${deque.peekFront()}`); // 2
console.log(`tail: ${deque.peekBack()}`); // 4
deque.popFront();
deque.print(); // 1-3-4
deque.popBack();
console.log(`length: ${deque.length()}`); // 2
deque.print(); // 1-3
```

# Ref

- [자바스크립트(JavaScript) 자료구조 Deque 구현해보기](https://jinhyukoo.github.io/js/2020/07/30/Deque_Javascript.html)
