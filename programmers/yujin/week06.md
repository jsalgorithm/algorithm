# 알고리즘 6주차

### 문제1 [ Design Circular Deque](https://leetcode.com/problems/design-circular-deque/)

```js
/**
 * Initialize your data structure here. Set the size of the deque to be k.
 * @param {number} k
 */

var MyCircularDeque = function(k) {
    // deque와 maxSize를 선언
    this.deque = [];
    this.maxSize = k;
    
};

/**
 * Adds an item at the front of Deque. Return true if the operation is successful. 
 * @param {number} value
 * @return {boolean}
 */
MyCircularDeque.prototype.insertFront = function(value) {
    // deque의 length가 maxSize와 동일한지 확인. 
    // 동일할 경우 false.
    // 그렇지 않으면 unshift로 값을 추가하고 true를 반환
    if(this.deque.length === this.maxSize){
        return false;
    }else {
        this.deque.unshift(value);
        return true;
    }
};

/**
 * Adds an item at the rear of Deque. Return true if the operation is successful. 
 * @param {number} value
 * @return {boolean}
 */
// deque의 length가 maxSize와 동일한지 확인. 
// 동일할 경우 false. 
// 그렇지 않으면 push로 값을 추가하고 true를 반환
MyCircularDeque.prototype.insertLast = function(value) {
    if(this.deque.lenght === this.maxSize){
        return false;
    }else {
        this.deque.push(value);
        return true;
    }
    
};

/**
 * Deletes an item from the front of Deque. Return true if the operation is successful.
 * @return {boolean}
 */
MyCircularDeque.prototype.deleteFront = function() {
    // deque의 length가 비어있는지 확인
    // 비어있다면 false. 
    // 그렇지 않으면 shift로 값을 제거하고 true
    if(this.deque.length === 0 ){
        return false;
    }else {
        this.deque.shift();
        return true;
    }
    
};

/**
 * Deletes an item from the rear of Deque. Return true if the operation is successful.
 * @return {boolean}
 */
MyCircularDeque.prototype.deleteLast = function() {
    // deque의 length가 비어있는지 확인
    // 비어있다면 false. 
    // 그렇지 않으면 pop으로 값을 제거하고 true
    if(this.deque.lenght === 0 ){
        return false;
    }else {
        this.deque.pop();
        return true;
    }
};

/**
 * Get the front item from the deque.
 * @return {number}
 */
MyCircularDeque.prototype.getFront = function() {
    // deque의 length가 비어있는지 확인
    // 비어있다면 -1을 반환. 
    // 그렇지 않으면 deque[0]을 반환
    
    if(this.deque.length === 0 ){
        return -1;
    }else {
        return this.deque[0];
    }
    
};

/**
 * Get the last item from the deque.
 * @return {number}
 */
MyCircularDeque.prototype.getRear = function() {
    // deque의 length가 비어있는지 확인
    // 비어있다면 -1을 반환. 
    // 그렇지 않으면 deque[length-1]을 반환
    if(this.deque.length === 0){
        return -1;
    }else {
        return this.deque[this.deque.length-1];
    }
};

/**
 * Checks whether the circular deque is empty or not.
 * @return {boolean}
 */
MyCircularDeque.prototype.isEmpty = function() {
    if(this.deque.length === 0 ){
        return true;
    }else {
        return false;
    }
    
};

/**
 * Checks whether the circular deque is full or not.
 * @return {boolean}
 */
MyCircularDeque.prototype.isFull = function() {
    return this.deque.length === this.maxSize;
    
};
```

### 문제2[23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)