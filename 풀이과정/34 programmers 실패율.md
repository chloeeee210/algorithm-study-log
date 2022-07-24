```jsx
// 뇌절뇌절 고민만 5G게 함
//핑구님 귯....😎
// # psudo
		// 아니 stage는 총 5개이지만 사용자가 클리어해서 도달할 수 있는 수는 N+1이다.
    // 일단 만드려는 배열의 길이는 5.왜냐면 stage의 개수가 N이기 때문에
    // [1,3,2,1,0] = stage에서 ~~i+1의 개수.~~1의 개수, 2의 개수, 3의 개수... N의 개수
    // [8,7,4,2,1] = stages.length에서 분모의 인덱스를 뺀 수 stages.length, stages.length - 분모[0], stages.length-분모 배열의 [1]
    /
    // ~~[1 - 7/8, 1 - 4/7, 1 - 2/4, 1 - 1/2, 1- 1/1]~~    
    // [0.125, 0.428, 0.5, 0.5, 0]
    // 각 e들을 내림차순으로 sort하여 해당하는 를 리턴함
    // [3,4,2,1,5]

    // 배열의 길이는 4 = N
    // [0,0,0,4]
    // [4,4,4,4]
```

```jsx
	// 고민한 것 = 반복문으로 구현하는 게 더 쉽겠다 싶었다! 왜냐하면 input값이 불변이면 메모리 ㄱ비효율..
	// 부수효과를 이용해야 하기 때문

// 삽질과정(1.5hr)
function solution (N, stages) {
    // 5-0, 5-1, 5-2, 5-3, 5-4 5-(5-i+1) N-1-i
    // 1,2,3,4,5
// 여기서 약간 N에 대한 새로운 range를 만들까 살짝 고민했는데
// N과 i의 관계를 이용해서 굳이 새로운 Range배열의 index로 조건식 걸어주기가 귀찮아서
// 이건.. 반복문을 써야 풀리겠구나 생각함.
// 그리고 위에서 써놓은 것처럼 중첩해서 length가 이전 index의 e를 뺀 수가 되버리면
// 이걸 reduce로 구현할 수 있을까?고민에 빠짐..
	// 아놔 ㅠ 분모 변수명 너무구림 ㅠ저게뭐야
   const bunmo = stages.filter((e,i)=> e == i ).length
}

// 아 그리고 모르겠는 거 또 있음
// 아니 filter를 돌려서 length 출력하는 걸 돌게하려면 어떻게해야함? 원본배열의 length가 아니라
// e == i로 filter한 숫자의 개수인데 이중배열로 만든다음에 그거의 Length를 출력하게하면되나?
// 근데 원본배열이아니라 (한번 판별식 돌린)배열을 가리킬 수가 없잖음 ㅠ e,i말고 다른매개변수없음?
// reduce는 콜백 돌리고 난 index(콜백돌림) index+1(콜백안돌림)의 e나 array를 가리킬수있는건가
```
## 디스캣님꺼 보고 공부한 풀이
```jsx
const range = (start, end) =>
  Array.from({ length: end - start + 1 }, (_, i) => i + start);

function solution(N, stages) {
	  const getBunmo = (x) => 
							stages
							.filter((y) => x <= y)
							.length;
		const getBunja = (x) => 
							stages
							.filter((y) => x == y)
							.length;
	  const getFailureRate = (bunja, i) => {
	    if (bunmoArr[i] === 0) return {rate : 0, stage : i+1};
	    return { rate: bunja / bunmoArr[i], stage: i + 1 };
	  };
	  const getSortedArr = (x) =>
							x.sort((a, b) => b.rate - a.rate)
							.map((e, i) => e.stage);
    
	const bunmoArr = range(1, N + 1).map((i) => getBunmo(i));
  const bunjaArr = range(1, N).map(getBunja);
  const failureRateArr = bunjaArr.map(getFailureRate);

	return getSortedArr(failureRateArr);
}
```