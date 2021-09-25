# 알고리즘 6주차

- 주제: 데크, 우선순위큐
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/09/06 ~ 09/12

## 목차

- 데크
  - 문제 1) [Leetcode - 641. Design Circular Deque](https://leetcode.com/problems/design-circular-deque/)
  - 문제 2) [백준 - 뱀](https://www.acmicpc.net/problem/3190) (너무 어려우면 대체할 것)
  - [Leetcode - 234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) (데크로도 풀 수 있음)
- 우선순위큐

  - 문제 1) [Leetcode - 23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
  - 문제 2) [Leetcode - 1337. The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/)

# 데크 문제 1 - 641. Design Circular Deque

- 문제 분류: `데크`
- 문제 출처: [Leetcode - 641. Design Circular Deque](https://leetcode.com/problems/design-circular-deque/)
- 라벨: `Medium`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/133609138-c98f4d71-61a4-459c-802e-e4e8f1638d00.png)

## 풀이

```js
var MyCircularDeque = function (k) {
  this.head = this.tail = null;
  this.maxSize = k;
  this.size = 0;
};

var Node = function (val) {
  this.prev = this.next = null;
  this.val = val;
};

MyCircularDeque.prototype._insertFirst = function (value) {
  this.head = this.tail = new Node(value);
  this.size++;
};

MyCircularDeque.prototype._deleteFirst = function () {
  this.head = this.tail = null;
  this.size--;
};

MyCircularDeque.prototype.insertFront = function (value) {
  if (this.size >= this.maxSize) return false;
  if (this.size === 0) {
    this._insertFirst(value);
    return true;
  }
  const node = new Node(value);
  node.next = this.head;
  this.head.prev = node;
  this.head = node;

  this.size++;
  return true;
};

MyCircularDeque.prototype.insertLast = function (value) {
  if (this.size >= this.maxSize) return false;
  if (this.size === 0) {
    this._insertFirst(value);
    return true;
  }
  const node = new Node(value);
  node.prev = this.tail;
  this.tail.next = node;
  this.tail = node;

  this.size++;
  return true;
};

MyCircularDeque.prototype.deleteFront = function () {
  if (this.size <= 0) {
    return false;
  }
  if (this.size === 1) {
    this._deleteFirst();
    return true;
  }

  this.head.next.prev = null;
  this.head = this.head.next;

  this.size--;
  return true;
};

MyCircularDeque.prototype.deleteLast = function () {
  if (this.size <= 0) {
    return false;
  }
  if (this.size === 1) {
    this._deleteFirst();
    return true;
  }

  this.tail.prev.next = null;
  this.tail = this.tail.prev;

  this.size--;
  return true;
};

MyCircularDeque.prototype.getFront = function () {
  return this.head ? this.head.val : -1;
};

MyCircularDeque.prototype.getRear = function () {
  return this.tail ? this.tail.val : -1;
};

MyCircularDeque.prototype.isEmpty = function () {
  return this.size === 0;
};

MyCircularDeque.prototype.isFull = function () {
  return this.size === this.maxSize;
};
```

- 시간 복잡도: 삽입, 삭제의 경우 모두 `O(1)`

![image](https://user-images.githubusercontent.com/33214449/132897799-76119400-cc7c-4201-96de-d1202e24381c.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/design-circular-deque/discuss/244615/JS-Doubly-Linked-List-solution)

# 데크 문제 2 -

- 문제 분류: `데크`
- 문제 출처: [Leetcode]()
- 라벨: ``, `JavaScript`

## 문제

## 풀이

## Ref

# 우선순위큐 문제 1 - 23. Merge k Sorted Lists

- 문제 분류: `우선순위큐`
- 문제 출처: [Leetcode - 23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)
- 라벨: `Hard`, `JavaScript`

> 이 문제의 해결방법에는 여러가지가 있다.
>
> - 우선순위큐나 최소히프
> - 분할 정복(Dived and Conquer)

## 문제

- k개의 연결 리스트(linked-list)가 담긴 `lists` 배열이 입력으로 들어온다. (각 연결 리스트는 오름차순으로 정렬되어있다.)
- 연결 리스트들을 오름차순으로 정렬된 한 개의 연결리스트로 합쳐 반환하여라.

## 풀이1

- `lists` 배열을 돌면서 2개의 리스트를 꺼내(shift) 오름차순이 유지되도록 합친다. 그리고 합친 연결리스트를 다시 `lists`배열에 넣는다. 이 과정을 반복하다보면 마지막엔 `lists`에 한 개의 연결리스트만이 남을 것이다. 이게 우리가 구하고자 하는 최종값이다.

```js
function mergeLists(a, b) {
  const dummy = new ListNode(0);
  let temp = dummy;
  while (a !== null && b !== null) {
    if (a.val < b.val) {
      temp.next = a;
      a = a.next;
    } else {
      temp.next = b;
      b = b.next;
    }
    temp = temp.next;
  }
  if (a !== null) {
    temp.next = a;
  }
  if (b !== null) {
    temp.next = b;
  }
  return dummy.next;
}

var mergeKLists = function (lists) {
  if (lists.length === 0) {
    return null;
  }

  while (lists.length > 1) {
    let a = lists.shift();
    let b = lists.shift();
    const h = mergeLists(a, b);
    lists.push(h);
  }
  return lists[0];
};
```

- 시간 복잡도: `O(n^2)`
  - `lists 배열의 원소 개수 x (배열의 원소인) 연결리스트의 길이` 만큼 걸림 (첫 `while`문 안에서 `mergeLists()`의 `while`문이 실행됨)

![image](https://user-images.githubusercontent.com/33214449/133610059-5c7f035a-9945-4607-8b45-f4b8fa4a2eb5.png)

## 풀이2(통과X)

자바스크립트는 자바처럼 우선순위큐와 관련된 내장 모듈 같은 게 없다. 그래서 자바스크립트로 최소 히프를 구현하여 이를 사용해봤다. 그러나 실행시켜보면 `JavaScript heap out of memory`라는 에러가 발생한다.(과도한 메모리 점유로 인한 에러) 런타임 에러로 제출되지 못한 코드이다.

```js
// min heap 사용
function ListNode(val, next) {
  this.val = val === undefined ? 0 : val;
  this.next = next === undefined ? null : next;
}

class Heap {
  constructor() {
    this.heap = [];
  }
  swap(indexA, indexB) {
    const temp = this.heap[indexA];
    this.heap[indexA] = this.heap[indexB];
    this.heap[indexB] = temp;
  }
  parentIndex(index) {
    return Math.floor((index - 1) / 2);
  }
  leftChildIndex(index) {
    return index * 2 + 1;
  }
  rightChildIndex(index) {
    return index * 2 + 2;
  }
  parent(index) {
    return this.heap[this.parentIndex(index)];
  }
  leftChild(index) {
    return this.heap[this.leftChildIndex(index)];
  }
  rightChild(index) {
    return this.heap[this.rightChildIndex(index)];
  }
}

class MinHeap extends Heap {
  add(node) {
    this.heap.push(node);
    this.heapifyUp();
  }

  remove() {
    const rootItem = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.pop();
    this.heapifyDown();
    return rootItem;
  }

  heapifyUp() {
    let curIndex = this.heap.length - 1;

    while (
      this.parent(curIndex) !== undefined &&
      this.heap[curIndex] < this.parent(curIndex)
    ) {
      this.swap(curIndex, this.parentIndex(curIndex));
      curIndex = this.parentIndex(curIndex);
    }
  }

  heapifyDown() {
    let curIndex = 0;

    while (
      this.leftChild(curIndex) !== undefined &&
      (this.leftChild(curIndex) < this.heap[curIndex] ||
        this.rightChild(curIndex) < this.heap[curIndex])
    ) {
      const smallerIndex =
        this.leftChild(curIndex) < this.rightChild(curIndex)
          ? this.leftChildIndex(curIndex)
          : this.rightChildIndex(curIndex);
      this.swap(curIndex, smallerIndex);
      curIndex = smallerIndex;
    }
  }

  isEmpty() {
    return this.heap.length === 0;
  }
}

var mergeKLists = function (lists) {
  const minHeap = new MinHeap();

  // heap에 연결리스트의 요소들 추가
  for (let list of lists) {
    let cur = list;
    while (cur) {
      minHeap.add(cur.val);
      cur = cur.next;
    }
  }

  let cur = new ListNode();
  // heap에서 하나씩 꺼내면서 새로운 연결리스트에 추가
  const head = cur;
  // console.log(head);

  //     console.log(minHeap.remove());
  //     console.log(minHeap.heap);
  while (!minHeap.isEmpty()) {
    cur.next = new ListNode(minHeap.remove());
    cur = cur.next;
  }

  //     console.log(head.next);

  return head.next;
};

const head1 = new ListNode(1);
head1.next = new ListNode(4);
head1.next.next = new ListNode(5);

const head2 = new ListNode(1);
head2.next = new ListNode(3);
head2.next.next = new ListNode(4);

const head3 = new ListNode(2);
head3.next = new ListNode(6);

const lists = [head1, head2, head3];
console.log(lists);
console.log(mergeKLists(lists));
```

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/merge-k-sorted-lists/discuss/114606/Extremely-simple-JavaScript-Solution) 풀이1 코드 참고
- [Leetcode Discuss](<https://leetcode.com/problems/merge-k-sorted-lists/discuss/10617/JavaScript-O(n-log-k)-time-and-O(k)-space-using-min-heap>)
- [[LeetCode, 리트코드] Merge k Sorted Lists](https://engkimbs.tistory.com/665) 자바, 히프를 사용한 풀이

# 우선순위큐 문제 2 - 1337. The K Weakest Rows in a Matrix

- 문제 분류: `우선순위큐`
- 문제 출처: [Leetcode - 1337. The K Weakest Rows in a Matrix](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/133609793-250f4d40-5c87-456e-b3ce-04a96d48ed71.png)

![image](https://user-images.githubusercontent.com/33214449/133609839-f45294dd-d7d1-4e7c-9d04-c8bfb2847c02.png)

- `m x n` 배열이 주어져있다. 값이 `1`이면 군인, `0`이면 시민을 나타낸다. (각 원소에서 무조건 시민보다 군인이 먼저 위치한다. `[1,1,1,0,0]`은 가능해도 `[0,1,0,1,1]`은 안된다는 뜻)
- 다음 조건을 충족할 때, `i`행이 `j`행보다 약하다고 말할 수 있다.
  - `i`행의 군인수(`1`의 개수)보다 `j`행의 군인수가 많을 때
  - 두 행의 군인수가 같다면 더 먼저 오는 행(인덱스가 작은 행)이 약한 것이다.
- 가장 약한 순서대로 `k`개의 행을 알아내고 이 행들의 군인 수를 배열에 담아 출력하라(예시를 보면 더 쉽게 이해가능하다.)

## 풀이

- 2차원 배열인 `mat`을 돌면서 `[인덱스, 1의 개수]` 형태의 원소를 가진 배열을 만든다.
  - 문제의 Example 1을 예시로 들면 `[[0,2], [1,4], [2,1], [3,2], [4,5]]` 이런 배열이 만들어질 것이다.
- `sort`를 이용해, 1의 개수가 작은 것부터 큰 순서대로 정렬한다. 1의 개수가 같을 경우 인덱스를 비교하여 순서를 정한다.
- 지금까지의 결과에서 인덱스값만 뽑아 배열을 만든다.
- 배열을 앞에서부터 k개만큼만 자른다.

```js
var kWeakestRows = function (mat, k) {
  return mat
    .map((row, index) => [index, row.filter((n) => n === 1).length])
    .sort(([i1, c1], [i2, c2]) => c1 - c2 || i1 - i2)
    .map(([index]) => index)
    .slice(0, k);
};
```

- 시간 복잡도: `O(n)`
  - `n`번 (=`mat`의 길이) 실행되기 때문이다. `.map(([index]) => index)`

![image](https://user-images.githubusercontent.com/33214449/132899574-a32021e2-881b-4844-8b36-5f0a10920081.png)

## Ref

- [Leetcode Discuss](https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/discuss/496819/JavaScript-Simple-solution)
