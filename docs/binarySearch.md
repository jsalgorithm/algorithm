# 이진탐색

이진탐색(binary search)란 정렬된 자료를 반으로 계속해서 나누어 탐색하는 방법입니다.

![binary search](https://t1.daumcdn.net/cfile/tistory/2452DE5057DEC4621E)

정렬된 배열에서 원하는 값을 찾기 위해 배열을 반씩 자른다.

![binary-search-2](http://michaelsyao.com/assets/images/binary-search-2.png)

주어진 배열에서 -1을 찾는 방법은 그림과 같다.

1. 전체 배열 중 가운데값을 찾는다 (middle = 3)
2. -1 < 3 이므로 가운데 값의 오른쪽을 탐색한다.
3. 가운데 값을 찾는다 (middle = 0)
4. -1 < 0 이므로 가운데 값의 오른쪽을 탐색한다.
5. 남은 한개의 데이터(-2) 와 비교연산한다.

자바스크립트 코드로 나타내면 아래와 같다.

```
function binarySearch(sortedArray, seekElement) {
	let startIndex = 0;
	let endIndex = sortedArray.length - 1;

// 무한 반복을 방지하기위한 조건문
	while (startIndex <= endIndex) {
		const middleIndex = Math.floor((endIndex + startIndex) / 2);
		// 타겟이라면 해당 값을 return한다.
		if (sortedArray[middleIndex] === seekElement) {
			return middleIndex;
		}
		// 타겟이 아니라면...
		if (sortedArray[middleIndex] < seekElement) {
			startIndex = middleIndex + 1;
		} else {
			endIndex = middleIndex - 1;
		}
	}

	return -1;
}

const nums = [10, 40, 50, 30, 60, 70, 80, 90, 20];
const sortedNums = nums.sort();

console.log(binarySearch(sortedNums, 30)); // 2
```

## 시간복잡도

이진탐색에서의 Big O 는 logn 이다.

> 처음에 데이터 수가 n개일 때의 탐색과정에서 1회의 비교연산 진행
>
> 데이터 수를 반으로 줄여서 그 수가 n/2개일 때의 탐색과정에서 1회 비교연산 진행
>
> 데이터 수를 반으로 줄여서 그 수가 n/4개일 때의 탐색과정에서 1회 비교연산 진행
>
> 데이터 수를 반으로 줄여서 그 수가 n/8개일 때의 탐색과정에서 1회 비교연산 진행
>
> ....
>
> 데이터가 1개 남았을 때 1회 비교연산 진행
> $$
> 첫 시행 시 \frac{N}{2}
> $$
>
> $$
> 두번째 시행 시 \frac{1}{2} * \frac{N}{2}
> $$
>
> $$
> 세번째 시행 시 \frac{1}{2} * \frac{1}{2} * \frac{N}{2}
> $$
>
> $$
> ...
> $$
>
> $$
> ( \frac{1}{2})^kN = 1 이 될 때 까지 시행
> $$
>
> $$
> 양 변에 2^k 를 곱해주면
> $$
>
> $$
> N = 2^k
> $$
>
> $$
> k = \log_2K
> $$
>
> 즉, 자료개수 N개에 따른 시간복잡도는 
> $$
> O \log N
> $$
> 으로 나타낼 수 있다.

이진탐색의 경우 시간복잡도가 로그형태로 나타나기 때문에, 100,000,000 개의 자료를 이진 탐색을 이용해 찾는다고해도

최대 8회의 연산 내로 결과를 도출할 수 있다.

만약 1억개의 자료를 선형탐색(linear search)한다면, 모든 자료에 대한 비교연산을 진행해야하기 때문에 1억번의 연산을 해야 할 것이다..

단, 반드시 정렬된 배열에 대해서만 적용이 가능하다.

따라서 링크드 리스트 등에 이진탐색을 사용하기 어렵다.

## 참고

https://www.fun-coding.org/Chapter16-binarysearch.html

https://jwoop.tistory.com/9

https://zelord.tistory.com/11