```jsx
// # [caution] 사고과정만 정리해서 안보셔도 됩니다 !
function solution(num) {
    let count = 0;
    // 0. 일단.. 연산을 500번보다는 적게 해야 함
    // 0.1 그리고 num 값이 1일 경우는 count를 1로 return해줌
    // 1. 먼저 num % 2가 1인지 0인지 (짝수인지 홀수인지) 판별한다.
    // 1.1 만약 num % 2 === 0 (num이 짝수면) num / 2를 하고
    // 결과값이 1이 아니라면 처음으로 돌아간다.
    // 1.2 만약 num % 2 === 1 (num이 홀수면) 3 * num + 1 를 하고
    // 결과값이 1이 아니라면 처음으로 돌아간다.

    // 몫 = quotient
    const quotient = num % 2;
		// 반복문 돌린다고 치면 
		// count++
		for (let count = 0; 참일때까지 루프를 도는 식; count++;) {
			if (quotient === 0) {
	      num = num / 2
	    }
	    if (quotient === 1) {
	      num = 3 * num + 1
	    }
	    if (num === 1) {
	      return count;
	    }
    return count;
		}
    
}
```

```jsx
//몽몽님의 설명을 듣고 작성해본 코드(💚몽몽님 감사합니다💚)
// 0. 일단.. 연산을 500번보다는 적게 해야 함
    // num 은 짝수고, 몫은 3이다. count = 0 
    // 1. 먼저 num % 2가 1인지 0인지 (= 홀수인지 짝수인지) 판별한다.
    // num = 3 , count = 1 -> 홀수
        //
        // 1.1 만약 num % 2 === 0 (num이 짝수면) num / 2를 하고
        //num = 3, count = 1
    
        // num이 1이 아니라면 처음(홀수인지 짝수인지 판별하는 시작점)으로 돌아간다.
        // 1.2 만약 num % 2 === 1 (num이 홀수면) 3 * num + 1 를 한다.
        //얘는 num값을 키우기만 한다.그래서 num값이 홀짝인지 판별하는 시점(=처음)으로 돌아갈 필요가 없다.
    
    // 2.1 연산을 모두 한 후, num이 1일 때의 연산의 count를 return한다.

        //참일 때 반복
    //-1을 리턴해줄때와 count가 500 이하일때가 없다!

function solution(num) {
    let count = 0;
    //num = 4, count = 0;
        //4번
//num = 4, count = 500;
        //참일 때 루프를 돈다.num = 1일때는 탈출!
        while( num != 1 ) {
            if(count>=500){
                return -1;
            }
            //둘 중 어느 연산을 하더라도 count를 해주어야 하기 때문에 여기서 count +=1을 먼저 해주는 것 (너무 명확한 몽님의 설명에 감동)
            count +=1 
            //if조건문은 해당되는 조건문을 만나면 해당되는 조건문만 실행이 되고 나머지 코드블록은 if를 탈출한다!(너무 명확한 몽님의 설명에 감동)
            // count >= 500이면, return -1 
            //짝수일때= 즉, 2로 나눴을 때의 나머지가 0일때
            if(num % 2 === 0){
            //num값을 나눠준다.
                num = num / 2
                //num =1, count = ??
                //1번 X
            } else  {
                num = (3*num) + 1    
                //count 값을 리턴할 수 없다 1이 절대로 ASKY
            }
                //2번 X
            
        } return count; //3번 
}
```