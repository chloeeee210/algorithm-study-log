# `정렬`
: 데이터를 특정한 기준에 따라 순서대로 나열하는 것.

## 선택정렬
: 처리되지 않은 데이터 중에서 가장 작은 데이터를 선택해 맨 앞에 있는 데이터와 바꾸는 것을 반복한다.
마지막 인덱스는 처리하지 않아도 데이터가 정렬을 완료한 상태가 된다.

선택 정렬은 N번 만큼 가장 작은 수를 찾아서 맨앞으로 보내야 한다.
N + (N-1) + (N-2) + ... +2 = N^2 + N - 2 / 2
`시간복잡도` : O(N^2)
```python
array = [1,2,3,8,3,7,6,5,4,8] [7]

for i in range(len(array)):
	min_index = i #가장 작은 원소의 인덱스
		if array[min_index] > array[j]:
			min_index = j
	array[i], array[min_index] = array[min_index] array[i] #swap

# 결과 [0,1,2,3,4,5,6,7,8,9]
```

## 삽입정렬
처리되지 않은 데이터를 하나씩 골라 적절한 위치에 삽입한다.
앞쪽에 있는 item이 정렬되어 있다고 가정하고 1번째 인덱스부터 어떤 위치로 들어갈 지 판단한다.

시간복잡도 : O(N^2).
삽입정렬은 현재 리스트(배열)의 데이터가 거의 정렬되어 있는 상태라면 매우 빠르게 동작한다.
최선의 경우 O(N)의 시간 복잡도를 가진다.
만약 모두 정렬되어 있다고 한다면 item이 어느 위치로 삽입될 지는 선형탐색을 시행하기 때문에 상수시간으로 대체된다.
```python
array = [7,5,9,8,3,1,6,2,4,8]
for i in range(1, len(array)):
	for j in range(i, 0, -1): # 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
		if array[j] < array[j-1]: #한 칸 시 왼 쪽으로 이동
				array[j], array[j-1] = array[j-1], array[j]
		else: #자기보다 작은 데이터를 만나면 그 자리에서 멈춤
			break
```

## 퀵 정렬
기준 데이터(피벗)를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법
기본적인 퀵 정렬은 첫 번째 데이터를 기준 데이터(Pivot)으로 설정한다.
피벗을 기준으로 데이터 묶음을 나누는 작업을 분할(Divide, Partition)라고 한다.
왼쪽 맨 끝에서부터 피벗값보다 큰 수, 오른쪽 맨 끝에서부터 피벗값보다 작은 수를 골라서 서로 위치를 바꾼다.
만약 바꾸다가 왼쪽에서 피벗값보다 작은수, 오른쪽에서부터 피벗값보다 큰 수를 선택하게 되었을 때(교차), 피벗의 위치와 피벗보다 작은 수의 위치를 바꾸고, 피벗값의 위치가 중간으로 와서 데이터가 분할된다.
시간 복잡도 O(NlogN)
너비 X 높이 = N X logN = NlogN
하지만 최악의 경우 O(N^2)의 시간복잡도를 가진다.
- 첫 번째 원소를 피벗으로 삼을 때, 이미 정렬된 배열에 대해서 퀵 정렬을 수행하면 어떻게 될까?(최악)

```python

arr = [6, 5, 1, 4, 7, 2, 3]
[6,5,1 ,4, 7,2,3]

[1, 2, 3] 4 [5, 6, 7]

def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    lesser_arr, equal_arr, greater_arr = [], [], []
    for num in arr:
        if num < pivot:
            lesser_arr.append(num)
        elif num > pivot:
            greater_arr.append(num)
        else:
            equal_arr.append(num)
    return quick_sort(lesser_arr) + equal_arr + quick_sort(greater_arr)
```


## 계수정렬(Counting Sort)
### `출처`
https://www.zerocho.com/category/Algorithm/post/58006da88475ed00152d6c4b

### `특징`
정렬할 수들의 `최대값`에 영향을 받는 알고리즘.
= 시간복잡도가 n의 크기에 따라 편차가 크다
**계수 정렬**은 **비교 정렬**이 아니다. 이전까지는 두 수를 비교하여 정렬했다면 이 방법은 단 하나의 비교도 일어나지 않았기 때문이다.
같은 숫자라도 정렬할 때 순서가 섞이지 않는 **안정 정렬** 중 하나이다.
정렬되기 이전 배열의 인덱스 순서대로 정렬을 하기 때문이다.

> -  **시간복잡도** :  `O(n+k)`
> 	k = 정렬할 수 중에 가장 큰 수
> 	n > k 일때의 시간복잡도 O(n)
> 	n < k 이고 k가 n보다 매우 큰 수일 때 O(∞)
> 		`예시`
> 		10개의 숫자를 정렬한다고 할 때 가장 큰 숫자가 100일 경우, 100(=k)는 10(=n)의 제곱이므로 O(n^2)가 된다.
> 		만약 k(가장 큰 숫자가) 1000이라면 시간복잡도는 O(N^3)이 된다. 1000이 10의 세 제곱이기 때문이다.

### `방법`
모든 숫자의 개수를 센 후, 누적 합을 구하고, 다시 숫자를 넣어주면 된다
> `예시`
	[3,4,0,1,2,4,2,4], [개수를 저장할 공간], [결과]  
> - 개수를 저장할 공간을 정렬할 제일 큰 수까지의 range.length를 0으로 채워준다.  
> (가장 큰 수는 4이고, 0부터 4까지 5개)
> 
	[3,4,0,1,2,4,2,4], [0,0,0,0,0], [결과] 
	- 가장 작은 수부터 개수를 센다.
	(0은 1개, 1은 1개, 2는 2개, 3은 1개, 4는 3개)
	>
	[3,4,0,1,2,4,2,4], [1,1,2,1,3], [결과]  
	- 각 숫자만큼의 개수를 [개수를 저장할 공간] 배열에 넣어준다.
	(개수를 저장할 공간 = 1,1,2,1,3)
	>
	[3,4,0,1,2,4,2,4], [1,2,4,5,8], [결과]  
	 [개수를 저장할 공간] 배열의 요소의 누적합으로 바꿔준다. 
	 (순서대로 1, 2, 4, 5, 8이 된다. [1,1,2,1,3].reduce((a,b)=> a+b))에서 각 e를 돌면서 호출되는 콜백의 리턴값)
	 >
	[3,4,0,1,2,4,2,4], [1,2,4,5,8], [결과]  
	누적합을 바탕으로 숫자를 결과에 넣어준다.
	0은 1에, 1은 2에, 2는 3~4에 3은 5에, 4는 6~8에 넣어주면 된다.
	>[0,  `1`, 1 , `2`, 2, 2, `4`, 3,  `5`, 4, 4, 4 , `8` ]
	>
	>
	>누적합이 숫자들의 인덱스 역할을 한다!
> `결과`
	[3,4,0,1,2,4,2,4], [1,2,4,5,8], [0,1,2,2,3,4,4,4]


누적합이 숫자들의 인덱스 역할을 한다! 라는 말을 한 번에 이해하지 못한 나를 위해 남겨놓는 예시
1,3,4,7이 있으면 1은 0~1 사이에, 2는 1~3 사이에, 3은 3~4 사이에, 4는 4~7 사이에 넣으라는 뜻

### `구현`
```javascript

const countingSort = function(array, k) {

	const count = [];
	const result = [];
	
	// 모든 숫자의 개수를 일단 0으로 초기화한다.
	for (let i = 0; i <= k; i++) { 
	count[i] = 0;
	}
	
	// 숫자의 개수를 세어 저장한다.
	for (let j = 0; j < array.length; j++) { 
	count[array[j]] += 1;
	}

	// 누적합을 구한다.
	for (let i = 0; i < k ; i++) { 
	count[i + 1] += count[i];
	}

	// 누적합이 가리키는 인덱스를 바탕으로 결과에 숫자를 넣는다.
	for (let j = 0; j < array.length; j++) { 
		result[count[array[j]] - 1] = array[j];
		count[array[j]] -= 1;
	}

	return result;

};
```
