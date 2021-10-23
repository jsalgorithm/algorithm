# Divide and Conquer
## 분할 정복 알고리즘?  
분할 정복 알고리즘은 그대로 해결할 수 없는 문제를 작은 문제들로 분할하여 작은 단위로 해결한 후, 이 해답들을 다시 합병하여 전체 문제를 해결하는 알고리즘이다. 대표적으로 Quick Sort, Merge Sort, 이진 탐색이 분할 정복 알고리즘에 해당된다.

### Quick Sort
[[자료구조 알고리즘] 퀵정렬(Quicksort)에 대해 알아보고 자바로 구현하기
](https://www.youtube.com/watch?v=7BDzle2n47c)

### Merge Sort
![](img/merge_sort.gif)

### 이진 탐색
![](https://blog.penjee.com/wp-content/uploads/2015/04/binary-and-linear-search-animations.gif)

## 분할 정복 알고리즘의 설계
1. Divide : 문제가 분할이 가능한 경우, 2개 이상의 문제로 나눈다.
2. Conquer : 나누어진 문제가 여전히 분할이 가능하면, 또다시 Divide를 수행한다. 그렇지 않다면 문제를 해결한다.
3. Combine : Conquer 한 문제들을 통합하여 전체 문제의 답을 얻는다.

## 분할 정복 알고리즘의 장단점
### 장점
- Top-down 재귀 방식으로 구현하기 때문에 코드가 직관적이다.
- 문제를 나누어 해결한다는 특성상 병렬적으로 문제를 해결할 수 있다.

### 단점
- 재귀 함수 호출로 오버헤드가 발생할 수 있다.
- 스택에 다량의 데이터가 보관되는 경우 스택 오버 플로우가 발생하거나 과도한 메모리를 사용할 수 있다.
