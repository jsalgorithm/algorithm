# 알고리즘 5주차

- 주제: 배열, 링크드 리스트
- 작성자: 박유림(Wol-dan) / @pul8219
- 작성일: 21/08/30 ~ 09/03

## 목차

- 배열
  - 문제 1) [Two Sum](Two-Sum)
  - 문제 2) [3Sum](#3Sum)
- 링크드 리스트
  - 문제 1) [Palindrome Linked List]()
  - 문제 2) [Swap Nodes in Pairs]()

# 배열 문제 1 - Two Sum

- 문제 분류: `배열`
- 문제 출처: [Leetcode - 1. Two Sum](https://leetcode.com/problems/two-sum/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/131692551-75ba8636-3d66-4f9f-a7ab-8c24aa937396.png)

- 입력: 정수들이 담긴 배열 `nums`
- 출력: `nums`에 들은 숫자들 중에서 더하면 `target`값이 되는 2개의 원소를 찾아 해당 원소들의 인덱스를 배열로 리턴. 한 원소를 두 번 사용하지 않고, 정답은 하나만 리턴하도록 한다.
- O(n^2)의 시간 복잡도 보다 적은 시간 복잡도로 해결할 수 있는지 고민해보기
- `nums`의 원소에는 음수도 올 수 있다.

## 풀이

- 중첩 for문을 사용해 문제를 풀었다.
- `nums` 배열의 첫 번째 원소부터 선택해가며 선택한 원소 뒤에 있는 원소와 더해서 `target`와 같은 값이 되는 두 원소를 찾는다.
- 선택한 원소 앞에 있는 원소들은 이미 비교해봤기 때문에 다시 비교하지 않아도 된다. 무슨 말이냐면,
  - nums = [2,7,11,15], target = 26 이라고 가정하면
  - 2 선택 -> [2, 7], [2, 11], [2, 15] 이렇게 두 원소를 선택하며 더하면 target 값이 되는지 확인
  - 다음 반복은 7 선택 -> [7, 11], [7, 15]
  - 11 선택 -> [11, 15]
  - 11 + 15 = 26 -> 답을 찾았으니 반복은 끝난다!

```js
var twoSum = function (nums, target) {
  for (let i = 0; i < nums.length - 1; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) {
        return [i, j];
      }
    }
  }
};
```

- 시간 복잡도: O(n^2)

![image](https://user-images.githubusercontent.com/33214449/131688615-abcb3bf1-f4d5-41cb-ae5b-9f58bc094040.png)

# 배열 문제 2 - 3Sum

- 문제 분류: `배열`
- 문제 출처: [Leetcode - 15. 3Sum](https://leetcode.com/problems/3sum/)
- 라벨: `Easy`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/131694606-8c9f4f6b-7699-44a1-b48c-78abbf384c73.png)

- 입력: 정수들이 담긴 배열 `nums`
- 출력: `nums` 배열에서 더하면 0이 되는 세 개의 원소를 배열로 리턴하기. 세 개의 원소는 각각 다른 원소이며(`i!=j`, `i!=k`, `j!=k`) 답은 여러 개일 수 있다. 그러나 중복되는 쌍은 포함하지 않도록 해야 한다.

## 풀이 1(통과X)

- 경우의 수를 나눠 생각했다. (더하면 0이 되는 경우. `-`는 음수, `+`는 양수 의미)
  - `-, -, +`
  - `-, 0, +`
  - `-, +, +`
  - `0, 0, 0`
- 중복되는 결과를 제외하기 위해서 배열에 `JSON.stringify()`를 적용한뒤 `Set`에 추가했다. 이렇게 중복이 제거되면 `Set`에서 꺼내면서 `JSON.parse()`로 자바스크립트 배열로 다시 변환했다.

```js
var threeSum = function (nums) {
  if (!nums.length) return [];
  if (nums.length === 1 && nums[0] === 1) return [];

  const neg = nums.filter((num) => num < 0).sort((a, b) => a - b); // 음수값만 배열에 담기
  const zero = nums.filter((num) => num === 0); // 0만 배열에 담기
  const pos = nums.filter((num) => num > 0).sort((a, b) => a - b); // 양수값만 배열에 담기

  let results = [];
  const set = new Set();

  if (zero.length >= 3) {
    results.push([0, 0, 0]);
  }

  // negative에서 두개를 뽑고 positive에서 한개를 뽑는 방법
  for (let i = 0; i < neg.length - 1; i++) {
    for (let j = i + 1; j < neg.length; j++) {
      const pick = pos.find((elem) => elem === Math.abs(neg[i] + neg[j]));
      if (pick) results.push([neg[i], neg[j], pick]);
    }
  }

  // positive에서 두개를 뽑고 negative에서 한개를 뽑는 방법
  for (let i = 0; i < pos.length - 1; i++) {
    for (let j = i + 1; j < pos.length; j++) {
      const pick = neg.find((elem) => elem === 0 - pos[i] - pos[j]);
      if (pick) results.push([pick, pos[i], pos[j]]);
    }
  }

  // negative에서 한개를 뽑고 positive에서 한개를 뽑고 0뽑는 방법 (애초에 0이 없으면 진행되지 않게 해야함)
  if (zero.length) {
    for (let i = 0; i < neg.length; i++) {
      const pick = pos.find((elem) => elem === Math.abs(neg[i]));
      console.log(pick);
      if (pick) results.push([neg[i], 0, pick]);
    }
  }

  // 결과에서 중복을 제거하기 위해 결과들에 JSON.stringify()한 값을 Set에 넣는다.
  results.forEach((result) => {
    set.add(JSON.stringify(result));
  });
  results = []; // results 초기화

  // Set에서 다시 꺼내며 최종적으로 리턴할 배열에 다시 추가
  for (let item of set) results.push(JSON.parse(item));

  return results;
};
```

- 시간 복잡도: O(n^3)

![image](https://user-images.githubusercontent.com/33214449/131703692-695ffde7-9bbd-4226-9289-4f026f1e01cb.png)

테스트 케이스는 통과하지만 시간이 너무 오래 걸려 통과되지 못했다.

## 풀이 2

문제를 못 풀겠어서 LeetCode Discussion에 있는 자바스크립트 솔루션을 코드를 따라가며 이해하려고 노력했다.
[참고한 코드 링크](https://leetcode.com/problems/3sum/discuss/281302/JavaScript-with-lots-of-explanatory-comments!)

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
function threeSum(nums) {
  const results = [];

  if (nums.length < 3) return results; // 이 코드는 nums에 적어도 3개의 숫자는 있어야 동작한다. 3개 미만이라면 빈 배열 리턴

  nums = nums.sort((a, b) => a - b); // 오름차순 정렬

  let target = 0;

  // k가 undefined가 되는 경우를 막기 위해서 nums.length - 2에서 반복을 멈춘다.
  for (let i = 0; i < nums.length - 2; i++) {
    if (nums[i] > target) break; // i는 왼쪽부터 시작한다. 그런데 이 값이 0보다 크다면 더 검사할 필요가 없으니 break한다. 양수만 있으면 0을 만들지 못하기 때문이다. (nums를 위에서 정렬했기 때문에 가능한 일) 0은 되는 이유는 [0,0,0]이라는 경우의 수가 있을 수 있기 때문

    // i번째 값이 이미 전에 봤던 값이라면 skip (반복된 결과를 피하기 위함)
    if (i > 0 && nums[i] === nums[i - 1]) continue;

    // j는 i 다음 값으로, k는 가장 오른쪽에 있는 값으로 시작한다.
    let j = i + 1;
    let k = nums.length - 1;

    // i는 겉의 for문에서 정해지고(for반복의 턴마다 고정됨) 아래 while문에서 j, k를 변화시켜나가며 값을 찾을 것이다. 아래 while문에서는 i는 고정되어있는 것이다. i는 처음, k는 끝에서부터 시작하고 j는 i와 k사이에 있는 값이다. j가 k와 같아지거나 k값을 넘어가면 아래 while문 반복을 종료한다.
    while (j < k) {
      let sum = nums[i] + nums[j] + nums[k];

      // 더해서 0(target)이 되는 값을 찾으면,
      // j를 증가시키고 k를 감소시킨다.
      if (sum === target) {
        // 더해서 0이 되는 경우의 수 이므로 결과에 push한다.
        results.push([nums[i], nums[j], nums[k]]);

        // 이미 (고정된)i와 j,k자리의 원소의 합이 sum이 되어 결과에 푸시되었다.
        // 이후 j와 k가 중복되는 값이 이어진다면 skip 해야한다.
        while (nums[j] === nums[j + 1]) j++;
        while (nums[k] === nums[k - 1]) k--;

        // 이제 진짜 다음 j, k로 넘어가는 작업이 필요하므로 아래 증감식을 추가한다.
        j++;
        k--;

        // sum 값이 0보다 작으면, j를 증가시킨다.(sum이 0에 가까워져야하기 때문에)
      } else if (sum < target) {
        j++;

        // sum이 0보다 크면, k를 감소시킨다.(sum이 0에 가까워져야하기 때문에)
      } else {
        k--;
      }
    }
  }

  return results;
}
```

# 링크드 리스트 문제 1 - Palindrome Linked List

- 문제 분류: `링크드 리스트`
- 문제 출처: [Leetcode - 234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
- 라벨: `Easy`, `JavaScript`

## 문제

- 입력: 단일 연결 리스트의 `head`
  - 입력값이 단순 배열인 것 같지만 입력값으로 들어오는 건 `head`노드이다. `head`노드의 `next`를 출력하면 연결 리스트의 두 번째 노드가 나올 것이다.
- 출력: 해당 연결 리스트의 노드의 값들이 앞에서부터 보나 뒤에서 부터 보나 같을 경우 `true`를 리턴하고 그렇지 않으면 `false`를 리턴 (like `토마토`는 거꾸로 읽어도 `토마토`)
  - 예를 들어 연결리스트가 `1->2->2->1` 이라면 이 연결리스트는 뒤에서부터 봐도 `1->2->2->1`이다. 그러므로 `true`를 리턴할 것이다.

## 풀이

- 재귀적인 방법으로 풀이 ([참고한 코드 링크](https://duncan-mcardle.medium.com/leetcode-problem-234-palindrome-linked-list-javascript-fc7293155c11))
- 함수를 재귀적으로 호출해가며 링크드 리스트의 끝값과 링크드 리스트의 맨앞값을 비교한다. 이후 링크드리스트의 중앙쪽으로 차례로 비교해나간다.
  - 재귀적으로 구현된 함수의 종료조건은 링크드 리스트의 끝을 만났을 때다.

```js
var isPalindrome = function (head) {
  function isPalindromeRecursive(recursiveHead) {
    // Reached the end of the list
    if (recursiveHead == null) {
      return true;
    }

    const next = isPalindromeRecursive(recursiveHead.next);

    const valid = recursiveHead.val === head.val;

    head = head.next;
    return next && valid;
  }
  return isPalindromeRecursive(head);
};
```

링크드 리스트가 [1,2,1]인 예시로 코드가 실행되는 과정을 따라가보면 다음과 같다.

![image](https://user-images.githubusercontent.com/33214449/131879184-c81a84d3-d242-423a-9d29-349f178cf006.png)

![image](https://user-images.githubusercontent.com/33214449/131879151-9bae14ee-ed0b-4f33-8234-1455518d3c39.png)

- 시간 복잡도: ?

![image](https://user-images.githubusercontent.com/33214449/131879398-61652460-253d-4b46-bdc1-5237fd0554e1.png)

## 다른 풀이들(참고하기)

- 링크드 리스트의 데이터를 배열에 저장해서 해결하는 방법

```js
var isPalindrome = function (head) {
  // Store all values from the linked list in an array
  let valuesFound = [];
  while (head) {
    valuesFound.push(head.val);
    head = head.next;
  }

  // Check if the list of values are a palindrome
  let left = 0;
  let right = valuesFound.length - 1;
  while (left <= right) {
    if (valuesFound[left] !== valuesFound[right]) {
      return false;
    }
    left++, right--;
  }

  return true;
};
```

![image](https://user-images.githubusercontent.com/33214449/132098074-8e627452-652b-4904-9602-09edb5f50da5.png)

# 링크드 리스트 문제 2 - Swap Nodes in Pairs

- 문제 분류: `링크드 리스트`
- 문제 출처: [Leetcode - 24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
- 라벨: `Medium`, `JavaScript`

## 문제

![image](https://user-images.githubusercontent.com/33214449/132098537-2c4f35dc-8507-4b7b-a90e-013e0a51d15e.png)

![image](https://user-images.githubusercontent.com/33214449/132098545-2bb1233d-ceec-46dc-8731-e36248718d31.png)

- 입력: 단일 연결 리스트의 `head`
  - 입력값이 단순 배열인 것 같지만 입력값으로 들어오는 건 `head`노드이다. `head`노드의 `next`를 출력하면 연결 리스트의 두 번째 노드가 나올 것이다.
- 출력: 연결리스트의 인접한 두 노드를 swap(교환)하고 교환이 완료된 연결 리스트를 가리키는 `head`를 리턴한다.
  - 노드의 value를 바꾸는 것이 아니라 노드 자체를 바꾸는 방식으로 구현해야 한다.
  - 예를 들어 `[1,2,3,4]` 로 이루어진 연결리스트가 있을 때, 노드 `1`과 `2`를 swap하고 노드 `3`과 `4`를 swap하여 최종적으로는 `[2,1,4,3]`인 연결리스트를 반환한다.
  - 빈 연결리스트가 입력값으로 들어올 경우 빈 배열? or 빈 연결리스트?을 리턴한다.
  - 노드가 하나만 있는 연결리스트가 입력값으로 들어올 경우 배열에 한 노드만 담아? or 해당 연결리스트를 그대로? 리턴한다

## 풀이

- [참고한 코드 링크](https://leetcode.com/problems/swap-nodes-in-pairs/discuss/11046/My-simple-JAVA-solution-for-share)
- 포인터 2개(dummy, point)가 첫 노드를 가리키도록 한다.
- 포인터 하나(point)를 갱신해가며 인접한 두 노드를 swap한다.
- 더이상 swap할 노드 2개가 없거나 남은 노드가 1개만 있을 경우 작업을 종료한다.
- 그림으로 보는 것이 이해가 더 빠를 것이다.

```js
var swapPairs = function (head) {
  const dummy = new ListNode(0);
  dummy.next = head;
  let point = dummy;
  while (point.next != null && point.next.next != null) {
    const swap1 = point.next;
    const swap2 = point.next.next;
    point.next = swap2;
    swap1.next = swap2.next;
    swap2.next = swap1;
    point = swap1;
  }
  return dummy.next;
};
```

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_2.jpg)

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_3.jpg)

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_4.jpg)

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_5.jpg)

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_6.jpg)

![image](https://windliang.oss-cn-beijing.aliyuncs.com/24_6.jpg)

- 시간 복잡도: O(n)

![image](https://user-images.githubusercontent.com/33214449/132102214-1092f1ff-a5b2-499d-b0b8-2814a5d1ba0a.png)
