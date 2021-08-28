# 4주차 알고리즘
## Maximum Depth of Binary Tree
### 코드 및 풀이
```javascript
//이진트리
//이런식으로 재귀 코드를 작성하고 생각하는 것이 더 쉽기 때문에 핸들러 함수를 사용

var maxDepth = function (root) {

    //깊이의 정의 때문에 숫자/깊이 값 1에서 시작

    return maxDepthHandler(root, 1)



};

//빈 root가 있으면 tree에는 아무것도 없으로 0깊이로 반환한다

var maxDepthHandler = function (root, num) {

    if (root == null) {

        return 0

    }

    if (root.right == null && root.left == null) {

        return num

    }

    //Math.max를 사용하여 두 루트 깊이에서 가장 높은 값을 얻는다.

    //나머지 코드 부분은 개별 루트 케이스를 처리

    if (root.right && root.left) {

        return Math.max(maxDepthHandler(root.right, num + 1), maxDepthHandler(root.left, num + 1))

    } else if (root.right != null) {

        return maxDepthHandler(root.right, num + 1)

    } else {

        return maxDepthHandler(root.left, num + 1)

    }

};
```
***
## Diameter of Binary Tree
### 코드 및 풀이과정

+ 트리의 지름 = 가장 멀리 떨어져있는 두 노드의 거리
+ 최대한 떨어져있는 두 노드의 거리를 구하는 문제
```javascript
var diameterOfBinaryTree = function(root) {
    let max = 0
    function maxDepth(root){
        
        if(root == null) return 0 // root가 null이면 0을 리턴
        let left = maxDepth(root.left) // 트리의 왼쪽 left에 할당한다( maxDepth(root.left)를 쓰는 대신 호출하는게 더 쉬울것이다.)
        let right = maxDepth(root.right) //위와 동일한 이유로 쓰기편하게 선언해준다
    
        max = Math.max(max, left + right)//경로가 루트를 통과하지않으면 최대값을 얻음
        return Math.max(left, right) +1 //경로는 루트를 통과하므로 1을 추가함
    
    }
    //경로가 루트를 지나갈지 안갈지 모르기때문에 => 루트를 지나가는 경로, 루트를 지나가지 않는 경로 사이의 최대값을 얻어야함
    maxDepth(root)
    return max
    
};
```


