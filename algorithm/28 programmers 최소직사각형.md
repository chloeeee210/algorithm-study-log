```jsx
```//# psudo
 // input [[60, 50], [30, 70], [60, 30], [80, 40]]
//이차원 배열에서 꺼내서 일렬로 값비교?(근데어차피 구조분해할당하려면 index를 사용해야함.. 일렬로 못꺼낼듯) 
// vs 0과 1번 인덱스를 돌면서 토너먼트처럼 값비교?

// # 고민.. 토너먼트처럼 값 비교? vs 일렬로 값 비교?
// 1.모든 배열에있는 item중 가장큰수를 찾고
// 2. 이차원배열의 element(배열)의 인덱스 0번과 1번을 비교해서 큰 값을 뱉는 array를 만들고
// 그 array의 최댓값을 찾음
// 3. 2번에서 작은 값 중에서 가장 큰거 찾으면 됌~

```

```jsx
function solution(sizes) {
    // input [[60, 50], [30, 70], [60, 30], [80, 40]]
	  // output 4000
    // 배열안에 배열이니까 배열의 element를 구조분해할당으로 꺼내서 두개의 값을 비교해야겠다
// Math.max 구현체 ? 반복문 돌리면서 처리함!
// 변수명 다시 짓기
    const longItem = sizes.map(([a,b])=> Math.max(a,b))
    const shortItem = sizes.map(([a,b])=> Math.min(a,b))
// 장지갑 컨셉임 세로가 더 길어요
    const vertical = Math.max(...longItem)
    const row = Math.max(...shortItem)
	return vertical*row

}
```