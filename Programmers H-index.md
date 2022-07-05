
# JS
```js
function solution(citations) { 
	const arr = citations.sort((a,b)=> b-a)
						 .findIndex((num, i)=> num <= i)
	
	return arr == -1 ? citations.length : arr
	}

```

# 💝💝💝💝💝python For 직님💝💝💝💝💝
```python
def solution(citations): 
	return max([min(i+1,sorted(citations, reverse=True)[i])
				for i in range(len(citations))])
```

# 구현 방법에 따른 시간복잡도

`이진탐색`일 경우
이미 정렬을 한 시점에서 O(nlogn)의 시간복잡도를 가지게 되고, 이진탐색을 적용한다고 해서 효율면에서 큰 차이가 없기 때문에 (**그리고 구현 못할 거 같아서 ㄱ-**) 이진탐색으로 구현하지 않았습니다.
자바의 스레드 사용이 자연스럽다면 이진탐색으로 병렬연산을 할 수 있을 것 같습니다…
이진탐색시 최악의 경우에 O(nlogn)로그의 밑은 2, 최선의 경우에(logn)의 시간복잡도를 가지고
`선형탐색`을 했을 시엔 O(n)을 가집니다.

-   **Binary Search시**
sort (nlogn)
h-index를 찾는 과정 = log n or n log N(최소~최대)
-   **linear search 시**
sort (nlogn)
h-index를 찾는 과정 = O(N)의 시간복잡도를 가지게 됩니다.

# Sort를 하지 않을 경우의 시간복잡도

sort를 하지 않은 citations 배열에서 인덱스+1한 값보다 작거나 같은 인용횟수를 찾는다고 한다면 시간복잡도가 O(N)이 아닌…O(N^2)가 되게 되어… 인생이 고통스러워집니다…