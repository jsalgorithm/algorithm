# Week 05

## 배열

- 문제 : https://leetcode.com/problems/two-sum/
- 풀이 1

```javascript
const twoSum = function (nums, target) {
	for (let i = 0; i < nums.length; i++) {
		for (let j = i + 1; j < nums.length; j++) {
			if (nums[i] + nums[j] === target) return [i, j];
		}
	}
};
```

- 풀이내용 :
  - 브루트포스법으로 풀이
  - 시간복잡도O(n^2)
- 풀이 2

```javascript
const twoSum = function (nums, target) {
	for (let i = 0; i < nums.length; i++) {
		let first = nums[i];
		let diff = target - first;
		if (nums.slice(i + 1).includes(diff)) return [i, nums.indexOf(diff)];
	}
};
```

- 풀이내용 :
  - 주어진 nums를 순회하면서, target에서 nuts[i]번째 값을 뺀 차이가 nums에 존재하는지 확인
  - 앞의 브루트포스법보다 시간이 더 오래걸렸음
    - 반복문을 이중으로 실행하고, slice, includes 메서드를 추가적으로 실행시켜야하기 때문이라고 생각

- 문제 : https://leetcode.com/problems/3sum/submissions/

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
const threeSum = function (nums) {
	let answer = [];
	nums.sort((a, b) => a - b);

	for (let i = 0; i < nums.length; i++) {
		if (i < 0 && nums[i] === nums[i - 1]) continue;

		// 투포인터를 이용한 계산
		let left = i + 1;
		let right = nums.length - 1;
		while (left < right) {
			let sum = nums[i] + nums[left] + nums[right];
			if (sum < 0) left++;
			else if (sum > 0) --right;
			else answer.push([nums[i], nums[left], nums[right]]);

			while (left < right && nums[left] === nums[left + 1]) left++;
			while (left < right && nums[right] === nums[right - 1]) --right;

			left++;
			--right;
		}
	}
	return answer;
};

console.log(threeSum([0, 0, 0, 0]));
```

- 풀이내용 :
  - 투포인터를 이용한 풀이
  - 각각 맨 처음과 끝을 점점 줄여나가며 탐색 범위를 줄여서 문제 풀이

----

## 링크드리스트

- 문제: https://leetcode.com/problems/palindrome-linked-list/

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {boolean}
 */
const isPalindrome = function (head) {
	const q = new Array();

	const node = head;
	// array 만들기
	while (head) {
		q.push(head.val);
		head = head.next;
	}
	console.log(q);

	while (q.length > 1) {
		if (q.pop() != q.shift()) {
			return false;
		}
	}

	return true;
};
```

- 풀이내용 :
  - 주어진 리스트를 array로 만듦.
    - ` head.val `을 순회하며 각각의 ` val `값을 ` array `에 ` push `한다.
    - 다음 node로 넘어가기위해 ` head = head.next `처리를 한다. 
  - pop, shift로 맨 처음값, 맨 끝값을 비교하며 풀이

----

- 문제 : https://leetcode.com/problems/swap-nodes-in-pairs/

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
const swapPairs = function (head) {
	let dummyList = new ListNode(null, head);
    console.log(dummyList)

	let current = dummyList;

	while (current.next && current.next.next) {
		const a = current.next;
		const b = current.next.next;

		//swap
		a.next = b.next;
		b.next = a;
		current.next = b;

		current = current.next.next;
	}
	return dummyList.next;
};
```

- 풀이내용:
  - value가 null인 노드를 추가한 dummyList를 생성한다.
  - 이 문제는 두 쌍의 노드의 위치만을 바꾸는 것이 아닌, 두 쌍의 노드 앞, 뒤의 노드또한 포인터를 변경해야한다.
  - 따라서 node.next(두 쌍의 노드 앞으로 이동 할 큰 값) , node.next.next(두 쌍의 노드 중 작은값이 가리킬 값) 이 존재하면 swap이 가능하다.
    - `a.next = b.next` : 작은값은 큰 값이 가리키던 값을 가리킨다.
    - `b.next = a` 큰 값은 작은값을 가리킨다.
    - `current.next = b` 작은값 직전의 노드는 b를 가리킨다.
    - `current = current.next.next` 다음 swap을 위해 이동한다.

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function(head) {
  var out = new ListNode(0);
  var now = out;

  out.next = head;

  while (now.next && now.next.next) {
    now = swap(now, now.next, now.next.next);
  }

  return out.next;
};

var swap = function (a, b, c) {
  a.next = c;
  b.next = c.next;
  c.next = b;
  return b;
};

```

