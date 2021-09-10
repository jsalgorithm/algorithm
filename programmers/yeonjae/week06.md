# 데크(deque)

- 양쪽 끝에서 삽입과 삭제가 모두 가능한 자료구조의 형태

- 문제 :  https://leetcode.com/problems/design-circular-deque/

- 코드

  ```javascript
  const MyCircularDeque = function (k) {
  	this.deque = [];
  	this.size = k;
  };
  
  // deque의 맨 앞자리에 값을 추가한다. 성공 시, true를 리턴한다.
  MyCircularDeque.prototype.insertFront = function (value) {
  	if (this.isFull()) {
  		return false;
  	}
  	this.deque = [...this.deque, value];
  	return true;
  };
  
  // deque의 맨 뒷자리에 값을 추가한다. 성공 시, true를 리턴한다.
  MyCircularDeque.prototype.insertLast = function (value) {
  	if (this.isFull()) {
  		return false;
  	}
  	this.deque = [value, ...this.deque];
  	return true;
  };
  
  // deque의 맨 앞에서 값을 삭제한다. 성공 시 true를 리턴한다.
  MyCircularDeque.prototype.deleteFront = function () {
  	if (this.isEmpty()) {
  		return false;
  	}
  	this.deque = this.deque.slice(0, this.deque.length - 1);
  	return true;
  };
  
  // deque의 맨 뒤에서 값을 삭제한다. 성공 시 true를 리턴한다.
  MyCircularDeque.prototype.deleteLast = function () {
  	if (this.isEmpty()) {
  		return false;
  	}
  	this.deque = this.deque.slice(1);
  	return true;
  };
  
  // deque의 맨 앞의 값을 가져온다.
  MyCircularDeque.prototype.getFront = function () {
  	if (this.isEmpty()) {
  		return -1;
  	}
  	return this.deque[this.deque.length - 1];
  };
  
  // deque의 마지막 값을 가져온다.
  MyCircularDeque.prototype.getRear = function () {
  	if (this.isEmpty()) {
  		return -1;
  	}
  	return this.deque[0];
  };
  
  // deque가 비어있는지 확인한다.
  MyCircularDeque.prototype.isEmpty = function () {
  	if (this.deque.length === 0) {
  		return true;
  	}
  	return false;
  };
  
  // deque가 꽉 찼는지 확인한다.
  MyCircularDeque.prototype.isFull = function () {
  	if (this.deque.length === this.size) {
  		return true;
  	}
  	return false;
  };
  
  ```

  - 풀이내용:
    - Slice() 메서드는 O(n)의 시간복잡도를 갖는다.
    - Push(), pop()의 경우 O(1)의 시간복잡도를 가지지만, myCircularDeque() 프로토타입 내에 정의되어있는 함수가 아니므로 사용할 수 없다.

  ---

  - 문제: https://leetcode.com/problems/palindrome-linked-list/
  - 코드

  ```javascript
  const isPalindrome = function (head) {
  	const queue = [];
  	if (!head) return true;
  
  	let node = head;
  
  	while (node !== null) {
  		queue.push(node.val);
  		node = node.next;
  	}
  
    while(queue.length > 1) {
      if(queue.shift() != queue.pop()) return false
    }
  
    return true
  };
  ```

  - 풀이내용:
    - 주어진 head를 배열로 만든다.
    - 배열의 길이가 1이 될 때 까지 shift()와 pop()을 이용해 배열의 앞, 뒤의 요소를 비교한다.
    - shift()는 시간복잡도가 O(N)이므로, 최대 O(N^2)의 시간복잡도를 가진다.

----

# 우선순위 큐(Priority queue)

- 순서 상관없이 우선순위가 높은 데이터가 먼저 나오는 것
- 힙으로도 구현 가능
- 문제 : https://leetcode.com/problems/merge-k-sorted-lists/
- 코드

```javascript
const mergeKLists = function (lists) {
	if (lists.length === 0) return null;
	return lists.reduce(mergeTwoLists);
};

function mergeTwoLists(a, b) {
	let c = new ListNode();
	let current = c;

	while (a && b) {
		if (a.val < b.val) {
			current.next = a;
			a = a.next;
		} else {
			current.next = b;
			b = b.next;
		}
		current = current.next;
	}
	current.next = a || b;
	return c.next;
}
```

- 풀이내용:

  - reduce 메서드로 list 내의 두 요소를 합친 후 그 값을 계속 누적해서 가져감

  - reduce(mergeTwoLists)는 mergeTwoLists의 반환값을 누산한다.

  - mergeTwoLists는 lists의 요소 a, b를 누적하면서 진행한다.

  - ```
    input = [[1,4,5],[1,3,4],[2,6]]
    
    mergeTwoLists(a,b) //a = [1,4,5], b = [1,3,4]
    while {
     a.val = 1 , b.val = 1
     current.next = b // c -> 1
     b = b.next // b.next = [3,4]
     current = current.next 
     
     a.val = 1, b.val = 3
     current.next = a // c -> 1 -> 1
     a = a.next // a = [4,5]
     current = current.next 
     
     ...
     
     current = [] -> 1 -> 1 -> 3 -> 4 , a = [4,5] b = []
     current = 1 -> 1 -> 3 -> 4, current.next = [4,5] // 내부노드는 모드 정렬된 상태
     1 -> 1 -> 3 -> 4 -> 4 -> 5
    }
    ```

---

- 문제:  https://leetcode.com/problems/the-k-weakest-rows-in-a-matrix/
- 코드:

```javascript
/**
 * @param {number[][]} mat
 * @param {number} k
 * @return {number[]}
 */
const kWeakestRows = function (mat, k) {
	let power = [];
	let answer = [];
	for (let i = 0; i < mat.length; i++) {
		let count = 0;
		let n = mat[i].length
		for (let j = 0; j < n; j++) {
			if (mat[i][j] === 1) count++;
		}
		power.push([i, count]);
	}
	power.sort((a, b) => a[1] - b[1]);

	for (let i = 0; i < k; i++) {
		answer.push(power.slice(0, k)[i][0]);
	}

	return answer;
};

```

- 브루트포스법을 이용한 풀이

### ref

https://medium.com/@ashfaqueahsan61/time-complexities-of-common-array-operations-in-javascript-c11a6a65a168