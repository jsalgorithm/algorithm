# 9주차 알고리즘
## Longest Repeating Character Replacement
### 문제 풀이
1. 창문의 범위를 지정하기 위해 `left`와 `right`를 선언한다. 초깃값은 둘 다 0으로 지정한다.
2. 창문의 범위 내에서 제일 많이 등장한 알파벳의 수를 저장하기 위해 `maxCharCount`를 선언한다. 초깃값은 0으로 지정한다.
3. 창문의 범위 내에서 알파벳의 수를 저장하기 위해 `visited`를 기록한다.
4. `right`(창문의 끝)가 `s`의 길이만큼 커질 때까지 `while` 문을 돈다. `right`는 반복문을 돌 때마다 1씩 커지도록 한다.
5. `right` 번째 알파벳의 등장 횟수를 `visited`에 기록하고, 창문 범위 내에서 가장 많이 등장했다면 `maxCharCount`를 업데이트한다.
6. 현재 범위의 알파벳 수 - 현재 범위에서 가장 많이 등장한 알파벳의 수 = **변경되어야 할 알파벳의 수**가 주어진 `k`보다 크다면 `left`를 증가시켜 창문을 오른쪽으로 이동시킨 후, `visited`에서 `left` 번째 알파벳의 수를 1 감소시킨다. (창문을 오른쪽으로 이동시키면서 첫 번째 알파벳을 잘라냈으므로)
7. 반복문을 모두 종료한 후, `right` - `left`(창문의 범위)를 반환한다.

### 시간 복잡도
O(n)

### 제출 코드
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
