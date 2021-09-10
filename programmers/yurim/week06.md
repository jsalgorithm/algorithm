# 알고리즘 6주차

- 주제: 데크, 우선순위큐
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/08/30 ~ 09/03

## 목차

- 데크
  - 문제 1) <https://leetcode.com/problems/design-circular-deque/>
  - 문제 2) <https://www.acmicpc.net/problem/3190> 너무 어려우면 대체
- 우선순위큐
  - 문제 1) <https://leetcode.com/problems/merge-k-sorted-lists/>
  - 문제 2) <https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/>
  - [Palindrome Linked List]() 데크로도 풀 수 있음

# 데크 문제 1 - 641. Design Circular Deque

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

![image](https://user-images.githubusercontent.com/33214449/132897799-76119400-cc7c-4201-96de-d1202e24381c.png)

## Ref

- https://leetcode.com/problems/design-circular-deque/discuss/244615/JS-Doubly-Linked-List-solution

# 우선순위큐 문제 1 - 1337. The K Weakest Rows in a Matrix

## 풀이

```js
var kWeakestRows = function (mat, k) {
  return mat
    .map((row, index) => [index, row.filter((n) => n === 1).length])
    .sort(([i1, c1], [i2, c2]) => c1 - c2 || i1 - i2)
    .map(([index]) => index)
    .slice(0, k);
};
```

![image](https://user-images.githubusercontent.com/33214449/132899574-a32021e2-881b-4844-8b36-5f0a10920081.png)

## Ref

- https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/discuss/496819/JavaScript-Simple-solution
