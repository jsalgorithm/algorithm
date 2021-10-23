617. Merge Two Binary Trees
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
var mergeTrees = function(root1, root2) {
    return merge(root1,root2);
};

function merge(root1,root2){
    //root1이 null일때 root2를 리턴
    if(root1 === null){
        return root2;
    }else if(root2 === null){
        //     root2가 null일때 root1을 리턴
        return root1;
    }
    
    root1.val+= root2.val;
    root1.left = merge(root1.left, root2.left);
    root1.right = merge(root1.right, root2.right);
    
    return root1;  
}
```


백트래킹1번 [Maximum Number of Balloons](https://leetcode.com/explore/challenge/card/september-leetcoding-challenge-2021/637/week-2-september-8th-september-14th/3973/)
```javascript
var maxNumberOfBalloons = function(text) {
    let counts = {b:0, a:0, l:0, o:0, n:0};
    for(let i = 0; i<text.length; i++){
        const c = text[i];
        if(counts[c] !== undefined) {
            counts [c]++;
        }
    }
    counts['l'] = Math.floor(counts['l']/2);
    counts['o'] = Math.floor(counts['o']/2);
    let minCount = Number.MAX_VALUE;
    for (let c in counts) { 
        if(counts[c] <minCount){
            minCount = counts[c];
        }
    }
    return minCount;
    
};
```
