# DFS, BFS

- 문제 : https://leetcode.com/problems/merge-two-binary-trees/

- 코드 : 

  ```javascript
  /**
   * Definition for a binary tree node.
   * function TreeNode(val, left, right) {
   *     this.val = (val===undefined ? 0 : val)
   *     this.left = (left===undefined ? null : left)
   *     this.right = (right===undefined ? null : right)
   * }
   */
  /**
   * @param {TreeNode} root1
   * @param {TreeNode} root2
   * @return {TreeNode}
   */
  const mergeTrees = function (t1, t2) {
  	if (t1 && t2) {
  		const newNode = new TreeNode(t1.val + t2.val);
  		newNode.left = mergeTrees(t1.left, t2.left);
  		newNode.right = mergeTrees(t1.right, t2.right);
  		return newNode;
  	}
  	return t1 || t2;
  };
  ```

  - 풀이내용 :
    - DFS 재귀함수로 풀이하였다. BFS의 경우 재귀풀이가 안된다.
    - t1, t2 노드가 존재하는 경우 `newNode` 에 `t1 + t2`를 `val`로 하는새로운 노드를 만든다.
    - 새로운 노드(`newNode`)의 left, right 속성에 대해  `mergeTrees` 에 대한 재귀를 한다.
      - `t1.left` 에 대해 `mergeTrees` 함수를 재귀한다. 
      - `t2.right`에 대해 `mergeTrees` 함수를 재귀한다.
    - 재귀가 모두 종료되면 newNode를 리턴한다.
    - 만약 두 노드 중 한 노드가 null이라면, null이 아닌 노드가 존재하는 트리를 리턴한다.

---

- 문제 : https://leetcode.com/problems/invert-binary-tree/

- 코드 :

  - 풀이 1

  ```javascript
  /**
   * Definition for a binary tree node.
   * function TreeNode(val, left, right) {
   *     this.val = (val===undefined ? 0 : val)
   *     this.left = (left===undefined ? null : left)
   *     this.right = (right===undefined ? null : right)
   * }
   */
  /**
   * @param {TreeNode} root
   * @return {TreeNode}
   */
  
  //recursion, dfs
  
  const invertTree = function (root) {
  	if (root === null) return root;
  	[root.left, root.right] = [invertTree(root.right), invertTree(root.left)];
  	return root;
  };
  
  ```

  - 풀이내용 :

    - DFS 재귀함수를 이용해 풀이. BFS는 재귀로 풀이할 수 없다.

    - inverTree의 인자가 null이 된 경우, 해당 인자를 반환한다.

    - null이 아닌 경우, [root.left, root.right]의 위치를 바꾼다.(구조분해할당)

      - 구조분해할당 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 한다.

        ```javascript
        let a, b;
        [a, b] = [10, 20];
        
        console.log(a);
        // expected output: 10
        
        console.log(b);
        // expected output: 20
        
        ```

      - 풀이 내용에서는 root.left, root.right 에 구조분해할당 구문을 이용하여 invertTree(root.right) , invertTree(root.left)를 할당한 것입니다.

      - https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment

  - 풀이2

    ```javascript
    const invertTree = function (root) {
    	let stack = [root];
    	let ret = [];
    	while (stack.length) {
    		const n = stack.pop();
    		if (n != null) {
    			[n.left, n.right] = [n.right, n.left];
    			ret.push(n.left, n.right);
    		}
    	}
    	return ret;
    };
    ```

  - 풀이내용 :
    - stack에 주어진 root값을 전부 담는다.
    - stack의 요소들을 하나씩 pop() 하면서, 해당 요소를 n에 할당한다.
    - n이 null이 아니라면, 구조분해할당 구문을 이용해 두 요소의 위치를 변경한다.(풀이1과 동일)
    - ret array에 해당 n.left, n.right 값을 push한다.
    - while문이 끝나면, root를 리턴한다.

----

# BackTracking

- 문제 : https://leetcode.com/explore/challenge/card/september-leetcoding-challenge-2021/637/week-2-september-8th-september-14th/3973/

- 코드 : 

  ```javascript
  var maxNumberOfBalloons = function(text) {
      let counts = {b:0, a:0, l:0, o:0, n:0};
      for(let i=0; i<text.length; i++) {
          const c = text[i];
          if(counts[c] !== undefined) {
              counts[c]++
          }
      }
      counts['l'] = Math.floor(counts['l'] / 2);
      counts['o'] = Math.floor(counts['o'] / 2);
      let minCount = Number.MAX_VALUE;
      for(let c in counts) {
          if(counts[c] < minCount) {
              minCount = counts[c]
          }
      }
      return minCount
  };
  ```

- 풀이내용 :
  - counts = {b:0, a:0, l:0, o:0, n:0} 인 객체를 생성한다.
  - 주어진 text의 길이만큼 반복문을 시행한다.
    - c = text[i] 에 해당하는 문자열을 할당한다.
    - counts객체 내에 c를 key로 하는 요소가 undefined가 아닌 경우, 해당 요소의 value를 1 증가 시킨다.
    - 'l','o'의 경우 두번씩 있으므로, 2로 나눈다.
    - minCount = Number.MAX_VALUE 를 할당한다.
      - Number.MAX_VALUE 는, 자바스크립트에서 나타낼 수 있는 가장 큰 수를 의미함
    - `for...i..in...`구문을 이용해 Counts객체의 Key에 대해 순회한다.
      - key값이 minCount보다 작으면, 해당 key를 minCount에 할당한다.
      - 최종적으로 minCount에는 key 중 최소값이 할당된다.
    - minCount를 리턴한다.
    - 백트래킹적으로는 못풀었다..