# week09



## 비트조작

- 문제 : https://leetcode.com/problems/hamming-distance/

- 코드

  ```javascript
  /**
   * @param {number} x
   * @param {number} y
   * @return {number}
   */
  const hammingDistance = function (x, y) {
  	x = x.toString(2);
  	y = y.toString(2);
  	const cal = x ^ y;
  	console.log(typeof cal);
  	let count = 0;
  	for (number of cal) {
  		if (number === 1) count++;
  	}
  
  	return count;
  };
  ```

  

- 풀이내용

  - `해밍거리` : 두 정수 또는 두 문자열의 차이를 의미한다.
  - ex : 1011101 , 1001001의 차이는 2이다.
  - 주어진 x와 y를 이진수로 변환한다.
    - 자바스크립트에서는 파이썬처럼 `bin` (이진수로 바꾸어주는 메서드)는 존재하지 않는다
    - 그러나 `toString(2)`메서드를 사용하면 이진수로 변환할 수 있다.
    - 두 수의 차이를 알기 위해 `XOR`연산을 하면 다른 숫자는 1이 될 것이다.
    - 따라서 XOR연산을 한 결과에서 1인 경우 count++하여 결과를 반환한다.

- 시간복잡도

  - 주어진 문자열을 이진수로 변경 후, for문을 통하기 때문에 시간복잡도는 O(n)이다.

----

- 문제 : https://leetcode.com/problems/single-number/
  - 주어진 배열 내 single number를 리턴하면 되는 문제였다.
- 코드

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const singleNumber = function (nums) {
	result = 0;
	for (let i = 0; i < nums.length; i++) {
		result ^= nums[i];
	}
	return result;
};
```



- 풀이내용

  - `XOR`연산을 이용해 풀이했다.
  - result 변수에 배열에 존재하는 숫자를 XOR연산하여 할당하였다.
  - 계속 반복하여 result에 XOR값을 할당하면, 같은 숫자인 경우, 0이 되지만 다른 숫자인 경우 1이 된다.
  - 결국 result값을 반환하면 nums배열의 여러가지 숫자 중 중복된 숫자들은 XOR연산으로 인해 0이 되고
  - Single number만 남게된다.

- 시간복잡도

  ​	O(n)

---

## 슬라이딩 윈도우

- 문제: https://leetcode.com/problems/contains-duplicate-ii/

- 코드

  ```javascript
  /**
   * @param {number[]} nums
   * @param {number} k
   * @return {boolean}
   */
  var containsNearbyDuplicate = function(nums, k) {
    const map = new Map();
    for (let i = 0; i < nums.length; i++) {
      if (i - map.get(nums[i]) <= k) {
        return true;
      }
      map.set(nums[i], i);
    }
    return false;
  };
  ```

  

- 풀이내용



- 문제 : https://leetcode.com/problems/longest-repeating-character-replacement/

- 코드

  ```javascript
  const characterReplacement = (s, k) => {
    let left = 0;
    let right = 0;
    let maxCharCount = 0;
    const visited = {};
  
    while (right < s.length) {
      const char = s[right];
      visited[char] = visited[char] ? visited[char] + 1 : 1;
  
      if (visited[char] > maxCharCount) maxCharCount = visited[char];
  
      if (right - left + 1 - maxCharCount > k) {
        visited[s[left]]--;
        left++;
      }
  
      right++;
    }
  
    return right - left;
  };
  ```

  

- 풀이내용

