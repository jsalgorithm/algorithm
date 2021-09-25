 # 이진트리(Binary Tree)와 이진트리 순회 방법(Binary Tree Traversal)
 
 ### 이진트리 : 부모 하나에 자식이 둘 딸린 구조 
 ![20210825_193114_3](https://user-images.githubusercontent.com/53229888/130909926-32af7b57-aaed-4fa9-b45d-ab490a499b8a.png)



## 1.1 이진트리 종류

### Binary Tree(기본)
![20210825_193114_4](https://user-images.githubusercontent.com/53229888/130910008-8f4dd85c-44f2-47c8-94a3-ca64fcdb80d9.png)



-   다른 조건 없이 자식노드가 2개씩만 붙어 있음됌

### Binary Search Tree
![20210825_193114_6](https://user-images.githubusercontent.com/53229888/130910458-9ed42bf5-e413-4f8d-a516-60e2608eaff6.png)

-   안에 데이터가 왼쪽 노드와 그 이하의 자식 도드들은 현재 노드 보다 작아야 함
-   오른쪽 노드와  그 이하 자식 노드들은  현재노드(8) 보다 커야함
-   만약 8보다 작은수를 찾고싶으면 왼쪽, 반대로 8보다 큰 수를 찾고싶으면 오른쪽으로 가면 된다.

### Balance
![20210825_193114_9](https://user-images.githubusercontent.com/53229888/130910544-0483ce7f-0411-4bbc-8e4f-355ed73e4cf9.png)


#### UnBalance
![20210825_193114_10](https://user-images.githubusercontent.com/53229888/130910565-5629698b-3152-4f3c-a7be-90f8632a5f50.png)

#### Complete Bianry Tree(완전이진트)
![20210825_193114_11](https://user-images.githubusercontent.com/53229888/130910589-70961882-5d13-4d41-bc28-9bc1735a4cbb.png)


-   모든 노드들이 왼쪽부터 채워져 있고 마지막 레벨은 왼쪽부터 채워져 있다

### Full Bianry Tree
![full](https://user-images.githubusercontent.com/53229888/130911127-8e5ae64e-91d2-4a52-ab82-db9432bfa2d2.png)

-   자식노드가 아예 없거나 2개로 구성된 Tree

### Perfect Bianry Tree

![prefect](https://user-images.githubusercontent.com/53229888/130911130-2073b321-12dc-4103-a49f-f329947964bf.png)


-   모든 노드가 2개의 자식노드로 구성된 트리 

## 1.2 이진트리 순회방법
![20210825_193114_2](https://user-images.githubusercontent.com/53229888/130910738-db12f3ab-9b80-49f2-a1d5-9d8fa5d4baaf.png)


### PreOrder(전위 순회)

-   현재노드 -> 왼쪽 서브 트리 -> 오른쪽 서브 트리 순으로 순회하는 방식 

1.  Root(==N)
2.  Left
3.  Right

### InOrder(중위 순회)

-   왼쪽 서브 트리 -> 현재노드 -> 오른쪽 서브 트리 순으로 순회하는 방식 

1.  Left
2.  Root
3.  right

### PostOrder(후위 순회)

-   왼쪽 서브 트리 -> 오른쪽 서브 트리 -> 현재노드 순회하는 방식 

1.  Left
2.  Right
3.  Root

***
참고링크 
- https://youtu.be/LnxEBW29DOw
- https://youtu.be/QN1rZYX6QaA
-
