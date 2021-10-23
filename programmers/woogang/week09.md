# 비트조작
## 136. Single Number

코드

```
const singleNumber = nums => {
  return nums.reduce((sum, current) => (sum ^= current));
};
```

문제풀이

XOR 연산을 사용

1.문제에서 중복되는 숫자가 있으면 2번 들어있으니 XOR로 배열의 모든 숫자를 계산한다.

2.XOR은 숫자를 2진수로 변환해 각 숫자가 같으면 0, 다르면 1로 나타내어지는 연산자이다.  
  같은 숫자를 비트 연산자로 계산하면 0이 됌.

3.결국 마지막에는 중복되지 않은 값 하나만 나와서 답을 구하게 된다.

## 461.Hamming Distance

코드

```
var hammingDistance = function(x, y) {
    let difference = x ^ y;  
    let distance = 0;
    
    while (difference > 0) {
        distance += difference & 1;  
        difference >>= 1;  
    }
    
    return distance;
};
```

문제풀이

1.XOR을 사용하여 비트 차이 찾기

2.가장 오른쪽 비트가 1이면 거리를 늘려준다.

3.쉬프트비트를 이용하여 오른쪽으로 1자리 이동해준다
