### 파이썬 알고리즘 인터뷰 : 해시테이블
> 해시테이블은 대부분의 연산이 분할 상환 분석에 따른 시간복잡도가 O(1)이라는 점이다. 279p, 파이썬 알고리즘 인터뷰

데이터 양에 관계 없이 빠른 성능을 기대할 수 있다는 장점이 있단다. 시간복잡도가 O(1)이기 때문.

>해시 함수란 임의의 크기 데이터를 고정 크기 값으로 매핑하는 데 사용할 수 있는 함수를 말한다.

맨 처음에 "해시"맵이라는 단어를 처음 보았을 때 "해시"란 유일한 값을 어떠한 내부적인 연산이나 처리를 해서 닝겐이 알아볼 수 형태로 암호화가 된 이런 의미를 떠올렸었는데 어떤 식으로 나의 자의적인 의미와 연결되는 지 의문이 들었다.

아무튼 해시 테이블의 핵심은 해시 함수라고 한다. 
입력값은 "ABC", "1234BC" "AF32B"이어서 각각 3글자, 6글자, 5글자이지만 특정 함수(해시함수)를 통과하면 2바이트의 고정 크기값으로 매핑된다. 이 역할을 하는 게 해시함수라고 한다.

```
ABC -> A1
1234BC -> CB
AF32B -> D5
```
## 해싱을 왜하는데?
이렇게 해시 테이블을 인덱싱하기 위해서 해시 함수를 사용하는 걸 해싱이라고 한다.
즉 정보를 가능한 한 빠르게 저장하고 검색하기 위해서 인 것임.

=> 내가 생각하지 못한 "해시" 일부분은 고정 크기 값으로 변형된다는 것이다~
그리고 이걸 인덱싱에 활용한다는 것~

그런데 `유일한`이 꽤 중요한 부분이었다!
성능 좋은 해시함수는 해시 함수 충돌을 적게 한다고 하는데... 이 책에서는 생일 문제를 예시로 들어서 설명한다.

한줄요약.txt
`해시함수를 돌린 결과값이 겹칠 경우 이를 충돌이라고 하고, (충돌을) 해결하는 방법에는 개별 체이닝과 오픈 어드레싱이 있다.`

그리고 이 책에서는 충돌이 일어나는 이유를 비둘기집 원리라는 귀여운 예시로 증명한다.
*비둘기집 원리*
> n개 아이템을 m개 컨테이너에 넣을 때, n>m이라면 적어도 하나의 컨테이너에는 반드시 2개 이상의 아이템이 들어있다는 원리를 말한다.

비둘기가 10마리이면 9개의 컨테이너 안에 적어도 1개의 컨테이너에는 2마리의 비둘기가 들어있을 것이다. (너무 상식적으로 당?연하다고 느껴질 수도 있지만 독일의 수학자 페터씨는 이걸 수학적으로 증명함)

아무튼 성능이 좋은 함수라면 적어도 들어오는 아이템의 개수가 10개라면 컨테이너가 9개밖에 없기 때문에 적어도 1번은 충돌 (해시함수를 돌린 값이 각기 다른 아이템을 가리키는 문제)하게 된다. 
그리고 성능이 좋지 않은 (해시)함수라면 최악의 경우 9번을 모두 충돌해서 9마리의 비둘기가 한 개의 컨테이너에 들어갈 수도 있다.
그래서 여러 번 충돌한다는 것은 그만큼 추가 연산을 필요로 하기 때문에 최소화하는 편이 좋단다~

> 로드 팩터(load Factor)
>  : 해시 테이블에 저장된 데이터 개수 n을 버킷의 개수 k로 나눈 것이다.
>  load factor = n/k

비둘기집 원리를 생각해보면 컨테이너 개수가 늘어날 수록 충돌할 확률이 적어지므로 이 지표는 해시 테이블의 크기를 재조정해야 하는지 또는 해시 함수를 재작성해야 할 지 결정하는 좋은 지표이다~
그리고 해시 함수가 키들을 잘 분산해주는지 효율을 측정하는 도구로써 사용된다고 한다.


책에서 해싱 알고리즘에 대해서 일일히 언급하려고 했지만 이 책의 범위를 벗어난다고 저자분이 흑염룡을 잠재웠다. 아쉽... 그냥 정보화시대에 검색하는데 0.1초도 안걸려서 검색해봄
> 암호학적 해시함수의 종류로는 [MD5](http://wiki.hash.kr/index.php/MD5 "MD5"), [SHA](http://wiki.hash.kr/index.php/SHA "SHA") 계열 해시함수가 있으며 비암호학적 해시함수로는 [CRC32](http://wiki.hash.kr/index.php/CRC32 "CRC32") 등이 있다.
> http://wiki.hash.kr/index.php/%ED%95%B4%EC%8B%9C%ED%95%A8%EC%88%98

다시 원점으로 돌아와서 이 충돌(collision)이 났을 때 어떻게 처리하는가? 
![[Pasted image 20220502163806.png]]
* 개별 체이닝 : 충돌 발생 시 연결리스트로 연결(link)
* 오픈 어드레싱 : 충돌 발생 시 선형탐사로 빈 공간을 찾아다니는 방식

`개별체이닝`
그림을 보자.
![[Pasted image 20220502164034.png]]
키 "윤아"와 "서현"이 해시된 값은 2를 가리키고, 충돌했다. 그래서 해시가 가리키는 2라는 값의 리스트를 만들어 2라는 해시값에 윤아(15)와 서현(17)을 리스트로 연결한 것인데 아니 그러면 복호화 했을 때 리스트의 인덱스도 저장하는 건가?


`오픈 어드레싱`
![[Pasted image 20220502164041.png]]
그림을 다시 보면 위 `개별체이닝`과 동일하게 키값 '윤아'와 "서현"이 해시값(해시함수를 실행한 후의 값)에서 충돌했다. 둘은 2를 가리키고 있기 때문이다.
그래서 "서현"은 다른 해시를 찾는다. 이 때 충돌한 해시값과 가까운 위치(메모리 주소상에서 가까운 위치)에서부터 찾기 때문에 `선형 탐색(linear probing)` 후 해시값을 3으로 가지게 된다.
> `선형탐색` : 충돌이 발생했을 때 해당 위치부터 순차적으로 탐사를 하는 방식

그래서 충돌했을 때 자신의 해시값과 다른 주소에 저장되지 않는 경우가 발생하기 때문에 조금 더 복잡한 것 같다.
그런데 이렇게 선형탐색을 거치게 되면 충돌한 메모리 주소값에서부터 **가까운** 메모리주소부터 탐색하기 때문에 해시테이블에 저장되는 데이터들이 한 쪽에 몰려서 분포하는 `클러스터링 (clustering)`이 발생하게 된다. 그러면 복호화 했을 때 해시를 뚫을 가능성도 같이 올라갈텐데... 뭐가 더 이득인지는 아직 내 지식수준에서 판단할 수가 없다
그리고 인덱싱을 거는 해싱까지 포함하면 다른 주소(위치)에는 데이터가 없는 상태가 되어버려서 탐사 시간이 오래걸리게 된다. (해싱 효율이 떨어짐)
그래서 오픈 어드레싱 방식은 버킷사이즈보다 데이터 양이 많은(큰)경우에는 삽입할 수 없다. 따라서 일정한 로드 팩터 비율을 넘어서게 되면 더 큰 크기의 또 다른 버킷을 생성한 후 새롭게 복사하는 `리해싱(rehashing)`작업이 일어난다고 한다.

`언어 별 해시 테이블 구현 방식`
![[Pasted image 20220502165453.png]]
지금 체이닝으로 구현한 방식(개별체이닝) VS 선형탐색(오픈어드레싱) 비교하면 조회 당 평균 캐시 실패횟수(?)가 선형탐색에서 현저히 낮다. 대신 로트팩터가 증가할 수록 조회 당 캐시 실패율이 올라가는데 이는 아까 전에 설명했던 리해싱을 하지 않았을 경우 버킷 사이즈보다 데이터의 크기가 더 큰 경우 해시의 성능이 구려지기 때문에 저렇게 지수함수스러운 모양이 나오는 것 같다(추측, 뇌피셜)

파이썬과 루비는 오픈어드레싱 방식으로 해시테이블을 구현했다고 한다~
C++이나 자바, 고는 개별 체이닝이라고 한다



---
7.12 update
# Object VS Map in JS
## Chrome status
https://stackoverflow.com/questions/18541940/map-vs-object-in-javascript

> Map objects are collections of key/value pairs where both the keys and values may be arbitrary ECMAScript language values. A distinct key value may only occur in one key/value pair within the Map’s collection. Distinct key values as discriminated using the a comparision algorithm that is selected when the Map is created.

> A Map object can iterate its elements in insertion order. Map object must be implemented using either hash tables or other mechanisms that, on average, provide access times that are sublinear on the number of elements in the collection. The data structures used in this Map objects specification is only intended to describe the required observable semantics of Map objects. It is not intended to be a viable implementation model.


## MDN

> A Map object can iterate its elements in insertion order - a `for..of` loop will return an array of [key, value] for each iteration.


