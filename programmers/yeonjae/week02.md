# 이진탐색(Binary search)

### Intersection of Two Arrays II

- https://leetcode.com/problems/intersection-of-two-arrays-ii/

```
const intersect = function (nums1, nums2) {
	const answer = [];
	let sortedArray = nums1;
	let justArray = nums2;
	if (nums1.length > nums2.length) {
		sortedArray;
		justArray;
	} else {
		sortedArray = nums2;
		justArray = nums1;
	}
	sortedArray.sort((a, b) => a - b);

	for (let i = 0; i < justArray.length; i++) {
		let startIndex = 0;
		let endIndex = sortedArray.length - 1;
		while (startIndex <= endIndex) {
			let middleIndex = Math.floor((startIndex + endIndex) / 2);
			let target = sortedArray[middleIndex];
			let value = justArray[i];
			if (target === value) {
				answer.push(target);
				sortedArray.splice(middleIndex, 1);
				break;
			} else {
				if (value < target) {
					endIndex = middleIndex - 1;
				} else {
					startIndex = middleIndex + 1;
				}
			}
		}
	}
	console.log(answer);
	return answer;
};

/* 해당 코드의 문제점:
	짧은길이의 array(이 예에서는 nums2)를 기준이 아닌 비교역으로 잡았기 때문에,
	[1,1]에서 첫번째 요소가 기준에 있으면 추가하고, 중복되는 일이 생김..
	문제에서 요구하는 바는 두 배열에 공통된 횟수만큼만 추가하는것이기 때문에
	기준이 되는 배열에서 하나씩 제거해줘야 함.
	여기서 기존에 알고있던 shift나 pop의 경우 각각 배열의 맨 앞, 맨 뒤의 요소를 삭제하는 것이기 때문에
	비교 대상인 middleIndex에 위치한 요소를 타겟팅하여 삭제하기 어려움.
	그래서 splice 메서드를 이용해서 타겟팅해 삭제함.
	splice이외에도 delete기능을 사용할 수 있지만,
	해당 기능은 요소는 존재하고 값만을 삭제하기 때문에 (undefined로 남음)
	필요없이 탐색을 해야한다. 그래서 splice를 사용했음.
*/
intersect([3, 1, 2], [1, 1]);

```

- 풀이 내용

  - 주어진 두개의 배열 중 긴 배열을 기준으로 잡았음.
    - 긴 배열의 중간값을 기준으로하고, 비교대상 배열로 for문을 돌면 시간복잡도가 더 줄어들 것이라는 예상때문
  - startIndex = 0, endIndex = 정렬된 배열의 길이 - 1
  - 이진탐색을 실시하여, 타겟을 찾으면 해당 값을 answer 배열에 추가하고 기준 배열에서 splice를 이용해 제거해 줌.
    - 두 배열의 공통된 횟수만큼만 answer에 추가하여야 하기 때문에, 기준 배열에 계속 남아있을 경우 한 쪽에만 중복된 요소가 answer에 중복된 횟수만큼 들어갈 수 있음
    - Ex: [3,1,2],[1,1] 의 경우, 기준배열 [1,2,3]과 비교배열[1,1]이 되고, 이진탐색을 하면서 1과 비교연산했을 때, 기준배열과 중복되어 answer = [1]되고, 그 다음 1과 비교연산 했을 때, 또 다시 중복되어 answer = [1, 1] 이 됨.

- 위 코드의 시간복잡도는 O(nlogn)이다. 이진 탐색을 시행하지만, 그 횟수는 for문만큼 이기 떄문이다..

  ### Find the duplicate Number

- 아직 못풀었다는.. 하;

# 해쉬(Hash)

### 완주하지 못한 선수

- https://programmers.co.kr/learn/courses/30/lessons/42576

```
function solution(participant, completion) {
	const HashTable = {};
	let key;

	for (key of participant) {
		if (!HashTable[key]) {
			HashTable[key] = 1;
		} else {
			HashTable[key] = HashTable[key] + 1;
		}
	}

	for (key of completion) {
		HashTable[key] = HashTable[key] - 1;
		console.log(HashTable);
	}

	for (key in HashTable) {
		if (HashTable[key]) {
			return key;
		}
	}
}

solution(
	["marina", "josipa", "nikola", "vinko", "filipa"],
	["josipa", "filipa", "marina", "nikola"]
);
```

- 위 문제를 푸는 방법 중 하나는 이중 for문을 돌리는 것이다.

  - for문을 두 번 돌려서, 참가자를 전부 배열에 넣고, 다음 for문에서는 완주자를 지운다거나.
  - 단, 이중 for문으로 시행할 때 시간복잡도는 O(n^2)

- 해쉬로 풀 경우, 시간복잡도는 줄고 공간복잡도는 늘어난다.

  - 저장의 경우 상수의 시간복잡도를 갖는다. O(1)

    - 해당하는 위치에 저장만 하면 되기 때문이다.
    - 단, 위의 경우처럼 해시 충돌이 일어나는 경우, O(n)의 복잡도를 갖게 될 수도 있다.

  - 검색의 경우 상수의 시간복잡도를 갖는다 O(1)
    - 해시값에 해당하는 값만 삭제하면 되기 때문이다.

### 위장

- https://programmers.co.kr/learn/courses/30/lessons/42578

```
function solution(clothes) {
	let key;
	const hashTable = {};
	for (let i = 0; i < clothes.length; i++) {
		key = clothes[i][1];
		if (!hashTable[key]) {
			hashTable[key] = 1;
		} else {
			hashTable[key] = hashTable[key] + 1;
		}
	}

	let result = 1;

	for (key in hashTable) {
		console.log(hashTable[key]);
		result = (hashTable[key] + 1) * result;
	}
	return result - 1;
}

solution([
	["yellowhat", "headgear"],
	["bluesunglasses", "eyewear"],
	["green_turban", "headgear"],
]);
```

- 위의 완주하지 못한 선수랑 비슷한 문제인데, 경우의 수 문제가 합쳐져서 헷갈릴 수 있다.

- 존재하는 경우의 수는 종류 별 옷을 섞어 입는 경우 + 아이템 하나만 착용하는 경우이기 때문이다.

- {headgear : 2, eyewear:1} 일 경우, 섞어입는 경우와 단독 아이템 착용의 경우를 모두 따져주기 위해서

- {headgear : [yellowhat,greenhae,none], eyewear: [bluesunglasese, none]} 처럼 아무것도 없는 경우까지 합해서 점화식을 세워준다. 단, none + none 조합을 제외한 점화식을 세운다.
