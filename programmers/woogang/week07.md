# BFS / DFS

## Merge Two Binary Trees

## 풀이방법

1.  t2를 t1에 병합한다
2.  노드 중 하나가 없으면 다른 노드를 반환하고 두 노드가 모두 존재하는 경우 값을 합산한다.
3.  왼쪽과 오른쪽 분기에 대해 동일한 작업을 해준다.
4.  합친 t1에 반환해준다.

```
var mergeTrees = function(t1, t2) {
    
    if (t1 === null) {
        return t2;
    }
    if (t2 === null) {
        return t1;
    }
    
    t1.val += t2.val;   
    t1.left = mergeTrees(t1.left, t2.left);
    t1.right = mergeTrees(t1.right, t2.right);  
   
    return t1;
};
```

# 백트래킹

## Maximum Number of Balloons

## 풀이방법

1.  모든 조합을 부분집합 해열로 만든다
2.  각각 xor연산을 적용

```
var subsetXORSum = function(nums) {
    const subsets = [[]]
    let sum = 0
    for(const el of nums){
        const last = subsets.length-1
        for(let i = 0; i<=last; i++){
            subsets.push([...subsets[i],el])
        }
    }
    
    for(let j = 0; j<subsets.length;j++){
        if (subsets[j].length === 0) sum = sum +0
        else if(subsets[j].length === 1) sum = sum + parseInt(subsets[j])
        else sum = sum + parseInt(subsets[j].reduce((acc,curr) => acc^curr))   
    }
    return sum
};
```
