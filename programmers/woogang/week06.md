# Merge Two Sorted Lists 

## 풀이방법
1. 연결 리스트 두 개를 값이 작은 순서대로 정렬하여 합친다.
2. 두 리스트는 이미 정렬되어 있으므로, 값을 비교해서 작은 값을 새 리스트에 추가해 나간다.

## 코드

```javascript
var mergeTwoLists = function(l1, l2) {
    // 빈 리스트가 있다면 합칠 필요가 없다.
    if(!l1) return l2;
    if(!l2) return l1;
    // 둘중에 더 작은값을 추가해서 새 리스트를 만들어 준다.

    let result = new ListNode();
    result.val = undefined; // 생성시 첫 val을 0이 들어가므로.. 첫 값을 초기화해준다.
    let nl1 = l1;
    let nl2 = l2;
    
    // l1, l2 중 한쪽이라도 값이 남아있는동안 계속 반복
    while(nl1 || nl2) {
        // 한쪽만 값이 남아있는 경우 
        if(!nl1) {
            while(nl2){
                result.add(result, nl2.val);
                nl2 = nl2.next
            }
            console.log('finish', result)
            return result;
        }
        if(!nl2) {
            while(nl1){
                result.add(result, nl1.val);
                nl1 = nl1.next
            }
            console.log('finish', result)
            return result;
        }
        
        // 더 작은 값을 result에 추가
        if(nl1.val < nl2.val){
            result.add(result, nl1.val);
            nl1 = nl1.next;
        } else {
            result.add(result, nl2.val);
            nl2 = nl2.next;
        }
        console.log(nl1, nl2, result)
    }
    return result;
};

ListNode.prototype.add = (node, val) => {
    var curr;
    if(node.val === undefined){
        node.val = val;
    } else {
        curr = node;
        while(curr.next){
            curr = curr.next
        }
        curr.next = new ListNode(val);
    }
}
```

# The K Weakest Rows in a Matrix

## 풀이방법
1. 배열을[index, 군인의 합계]형식으로 바꿔준다.
2. 배열 정렬 : 군인의 합계가 같으면 인덱스로 정렬해준다.
3. 정렬된 결과의 행 인덱스를 가져온다
4. K수에 따라 결과를 slice해준다.

## 코드
```javascript
var kWeakestRows = function (mat, k) {
  return mat
    .map((e, i) => [i, e.reduce((acc, cur) => acc + cur, 0)])	
    .sort((a, b) => (a[1] == b[1] ? a[0] - b[0] : a[1] - b[1]))	
    .map((x) => x[0])	
    .slice(0, k);
	
};
```
