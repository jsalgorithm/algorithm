# 이진탐색트리(Binary Search Tree)

![이진탐색트리 구조](https://simplesnippets.tech/wp-content/uploads/2020/10/binary-search-tree-featured-image.jpg)

이진탐색트리는 이진탐색(binary search)과 연결리스트(linked list)를 결합한 자료구조이다. 이진탐색은 탐색에 소요되는 시간복잡도가 O(logn)으로 빠른 편이나, 자료의 입력과 삭제가 불가능하다. 한편 연결리스트는 자료의 입력과 삭제에 소요되는 시간복잡도가 O(1)으로 효율적이나 탐색에 발생하는 시간복잡도는 O(n)이다. 즉, 이진탐색트리는 이진탐색과 연결리스트의 장점을 결합하였다고 볼 수 있다.

## 이진탐색트리 특성

- 모든 노드들은 중복되지 않는 고유한 값을 갖는다.
- 왼쪽 서브트리는 해당 노드보다 작은 값을 갖는 노드들로 구성된다.
- 오른쪽 서브트리는 해당 노드보다 큰 값을 갖는 노드들로 구성된다.
- 왼쪽과 오른쪽의 서브트리 또한 이진탐색트리이다.

> ❗️ 이진탐색트리의 단점
> 편향된 트리 구조일 경우, 최악의 시간복잡도는 O(n)으로 연결리스트와 동일한 성능을 보이기 때문에 이진탐색트리를 사용하는 의미가 없어진다.

![편향 이진 트리](https://blog.kakaocdn.net/dn/WfWhw/btqG6B0pmHy/Q5QGEcm7FMIxygZQgmLQbk/img.png)

## 이진탐색트리 중위순회(Inorder)

이진탐색트리를 순회할 때는 `왼쪽 서브트리` - `노드` - `오른쪽 서브트리` 순으로 중위순회 방식을 사용한다.

![이진탐색트리 중위순회](https://media.vlpt.us/images/taeha7b/post/b70d2d68-36cb-43a1-9e7b-ba80d2ae822c/%EC%A4%91%EC%9C%84-%EC%88%9C%ED%9A%8C.gif)

## 이진탐색트리 연산

### 탐색

1. 찾고자 하는 값을 루트 노드와 비교한다.
2. 찾고자 하는 값이 루트 노드보다 작으면 왼쪽 서브트리에서 재귀적으로 탐색한다.
3. 찾고자 하는 값이 루트 노드보다 크면 오른쪽 서브트리에서 재귀적으로 탐색한다.
4. 찾고자 하는 값과 루트 노드가 같으면 탐색을 종료한다.

### 삽입

1. 우선 삽입하고자 하는 값으로 탐색을 수행한다.
2. 탐색 후 일치하는 노드가 없으면 탐색을 실패한 위치가 곧 노드를 삽입할 위치가 된다.

![이진탐색트리 삽입](https://upload.wikimedia.org/wikipedia/commons/8/83/Binary-search-tree-insertion-animation.gif)

### 삭제

- 자식 노드가 없는 경우  
  해당 노드를 바로 삭제한다.

![이진탐색트리 삭제 1](https://i.giphy.com/media/ZcLLXw3CXlqGrFVtRi/giphy.gif)

- 자식 노드가 1개인 경우  
  해당 노드를 삭제하고 그 위치에 자식 노드를 가져온다.

![이진탐색트리 삭제 2](https://i.giphy.com/media/YrZ18grMiPQ6J2QWhP/giphy.gif)

- 자식 노드가 2개인 경우  
  해당 노드를 삭제하고 그 위치에 그 직전 값인 노드(=왼쪽 서브트리에서 가장 큰 값을 갖는 노드) 또는 직후 값인 노드(=오른쪽 서브트리에서 가장 작은 값을 갖는 노드)를 가져온다.

![이진탐색트리 삭제 3](https://i.giphy.com/media/S78Dap8pBddwvipsNi/giphy.gif)

## 자바스크립트로 구현한 이진탐색트리

```javascript
class Node{
  constructor(data){
    this.data = data;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree{
  constructor(){
    this.root = null;
  }
}

findMinNode(node){
  if(node.left === null) return node;
  else return this.findMinNode(node.left);
}

// 탐색
search(node, data){
  if(node === null) return null;
  else if(data < node.data) return this.search(node.left, data);
  else if(data > node.data) return this.search(node.right, data);
  else return node;
}

// 삽입
insert(data){
  var newNode = new Node(data);

  if(this.root === null) this.root = newNode;
  else this.insertNode(this.root, newNode);
}

insertNode(node, newNode){
  if(newNode.data < node.data>){
    if(node.left === null) node.left = newNode;
    else this.insertNode(node.left, newNode);
  }else{
    if(node.right === null) node.right = newNode;
    else this.insertNode(node.right, newNode);
  }
}

// 삭제
remove(data){
  this.root = this.removeNode(this.root, data);
}

removeNode(node, key){
  if(node === null) return null;
  else if(key < node.data){
    node.left = this.removeNode(node.left, key);
    return node;
  }else{
    // 1) 자식 노드가 없는 경우
    if(node.left === null && node.right === null){
      node = null;
      return node;
    }

    // 2) 자식 노드가 1개인 경우
    if(node.left === null){
      node = node.right;
      return node;
    }else if(node.right === null){
      node = node.left;
      return node;
    }

    // 3) 자식 노드가 2개인 경우
    var aux = this.findMinNode(node.right);
    node.data = aux.data;

    node.right = this.removeNode(node.right, aux.data);
    return node;
  }
}
```

[코드 설명 자세히 보기](https://www.geeksforgeeks.org/implementation-binary-search-tree-javascript/)
