# Linked list

## 선형 자료구조

- 선형 자료구조는 크게 물리적 메모리 내에 연속적으로 데이터를 저장하는 연속(Countinous)방식과, 포인터 기반의 연결(Linked) 방식이 존재 
- 링크드 리스트는 포인터 방식
- 배열과 비슷하지만, 각각의 데이터들은 메모리 내에 임의의 위치에 저장되어있으며 포인터, 혹은 다음 노드에 대한 데이터를 포함하는 자료구조

![](https://res.cloudinary.com/dvj2hbywq/image/upload/v1590572188/Group_14_5_bvpwu0.png)

- 링크드 리스트의 진입점은 head이고 첫번째 노드를 참조함
- 링크드 리스트의 종단점은 null을 참조함
- 각 노드는 데이터와 다음 데이터를 가리키는 공간을 포함

- 링크드리스트를 자바스크립트에서 보면 아래 코드와 같다.

```javascript
const list = {
    head: {
        value: 6
        next: {
            value: 10                                             
            next: {
                value: 12
                next: {
                    value: 3
                    next: null	
                    }
                }
            }
        }
    }
};
```

-----

## 구현하기

```javascript
class listNode {
	constructor(data) {
		this.data = data;
		this.next = null;
	}
}

class linkedList {
	constructor(head = null) {
		this.head = head;
	}
}

let node1 = new listNode(2);
let node2 = new listNode(5);
node1.next = node2;

let list = new linkedList(node1);

console.log(list.head.next.data);

```

----

## 링크드 리스트와 배열의 차이점

![](https://miro.medium.com/max/1400/1*sBUu3B4LnXxmKV1P5FVbWg.png)

- 배열
  - 데이터가 메모리에 연속적으로 저장
  - 따라서 메모리 크기를 미리 할당해야 함 (C언어 같은 저수준 언어의 경우)
  - 만약 데이터를 추가하여 크기를 늘릴 경우, 메모리 재할당 필요
  - 임의의 데이터에 접근하는 시간복잡도 O(1)
  - C와 같은 저수준 언어에서는 메모리 할당을 수동으로 함
  - 자바스크립트와 같은 고수준 언어에서는 동적할당을 함
  - 사용하지 않게 된 메모리에 대해서는 가비지 컬렉터가 해제
- 링크드 리스트
  - 물리 메모리를 연속적으로 사용하지 않아도 됨
  - 링크드 리스트는 메모리를 미리 할당 할 필요 없음
  - 리스트의 앞, 뒤에 데이터를 추가할 때 시간복잡도 O(1)
  - 임의의 데이터에 접근할 수 없음
  - 무조건 head부터 시작해서 데이터를 탐색해야하기 때문에 탐색은 시간복잡도 O(n)

---

## Ref

- https://www.freecodecamp.org/news/implementing-a-linked-list-in-javascript/



