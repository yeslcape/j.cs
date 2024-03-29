# 해시(Hash) / 해시 테이블(Hash Table)
![image](https://github.com/yeslcape/schedule/assets/45252618/5dd5dd7d-7cda-40fc-9095-07d0b5cb6630)

### 해시 함수 개념
해시 함수(hash function) 또는 해시 알고리즘(hash algorithm) 또는 해시함수 알고리즘은 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수를 의미

### 해시 개념
해시 함수에 의해 얻어진 값
입력 데이터를 고정된 길이의 데이터로 변환된 값
= 해시 값, 해시 코드, 체크섬

### 해시 테이블 개념
연관배열 구조를 이용하여 키(key)에 결과 값(value)을 저장하는 자료구조
cf) 연관배열 구조(associative array)란, 키(key) 1개와 값(value) 1개가 1:1로 연관되어 있는 자료구조

### 해시 테이블 구성
키(key)는 해시함수(hash function)를 통해 해시(hash)로 변경이 되며 해시는 값(value)과 매칭되어 저장소에 저장
* 키(key)
  * 고유한 값
  * 해시 함수의 input
  * 다양한 길이의 값이 될 수 있음
  * 해시 함수로 값을 바꾸어 저장 -> 공간의 효율성 추구
* 해시함수(Hash Function)
  * 키(key)를 해시(hash)로 바꿔주는 역할
  * 다양한 길이를 가지고 있는 키(key)를 일정한 길이를 가지는 해시(hash)로 변경하여 저장소를 효율적으로 운영할 수 있도록
  * 서로 다른 키(key)가 같은 해시(hash)가 되는 경우를 해시 충돌(Hash Collision)이라고 하는데, 해시 충돌을 일으키는 확률을 최대한 줄이는 함수를 만드는 것 중요!!
* 해시(Hash)
  * 해시 함수(Hash Function)의 결과물
  * 저장소(bucket, slot)에서 값(value)과 매칭되어 저장
* 값(Value)
  * 저장소(bucket, slot)에 최종적으로 저장되는 값
  * 키와 매칭되어 저장, 삭제, 검색, 접근 가능

### 해시 테이블 사용 이유
* 적은 자원으로 많은 데이터를 효율적으로 관리하기 위해
* 하드디스크나, 클라우드에 존재하는 무한한 데이터들을 유한한 개수의 해시값으로 매핑하면 작은 메모리로도 프로세스 관리 가능

### 특징
* 키(KEY)에 데이터(Value)를 매핑할 수 있는 데이터 구조
* 해시 함수를 통해 키의 데이터를 배열에 저장할 수 있는 주소(인덱스 번호) 계산
* 키를 통해서 저장된 데이터를 빠르게 찾고, 저장 및 탐색 속도가 획기적으로 빨라짐

## 장점
* 데이터 저장/조회 속도 빠름 
* 검색 속도 빠름
* 키에 대한 데이터가 있는지 확인 쉬움

### 단점
* 일반적으로 저장공간이 많이 필요
* 여러 키에 해당하는 주소(인덱스)가 동일한 경우 충돌을 해결하기 위한 별도 자료구조 필요
* 순서가 있는 배열에는 어울리지 않음
* Hash Function의 의존도 높음
  * 평균 데이터 처리의 시간복잡도는 O(1)이지만, 이는 해시 함수의 연산을 고려하지 않는 결과
  * 해시함수가 매우 복잡하다면 해시테이블의 모든 연산의 시간 효율성 증가

### 시간복잡도
* 충돌이 없는 경우 : O(1)
* 최악의 경우, 즉 모든 index에서 충돌이 발생할 경우 : O(n)
  * 함수 알고리즘의 성능이 좋지 못하여 발생
  * 저장되는 데이터 양이 해시 테이블의 크기(Size) 보다 클 때

### 해시 충돌(Hash Collision) 해결 방법
* Separate Chaining
  * 자료 저장 시, 저장소(bucket)에서 충돌이 일어나면 해당 값을 기존 값과 연결시키는 기법
  * 장점
    1) 한정된 저장소(Bucket)을 효율적으로 사용
    2) 해시 함수(Hash Function)을 선택하는 중요성이 상대적 적음
    3) 상대적으로 적은 메모리를 사용한다. 미리 공간을 잡아 놓을 필요가 없음
  * 단점
    1) 한 Hash에 자료들이 계속 연결된다면(쏠림 현상) 검색 효율을 낮출 수 있음
    2) 외부 저장 공간 사용
    3) 외부 저장 공간 작업을 추가로 해야함
* Open Addressing(개방주소법)
  * 비어있는 해시(hash)를 찾아 데이터를 저장하는 기법
  * 개방주소법에서의 해시테이블은 1개의 해시와 1개의 값(value)가 매칭되어 있는 형태로 유지
  * 선형 탐색(Linear Probing): 다음 해시(+1)나 n개(+n)를 건너뛰어 비어있는 해시에 데이터 저장
  * 제곱 탐색(Quadratic Probing): 충돌이 일어난 해시의 제곱을 한 해시에 데이터 저장
  * 이중 해시(Double Hashing): 다른 해시함수를 한 번 더 적용한 해시에 데이터 저장
  * 장점
    1) 또 다른 저장공간 없이 해시테이블 내에서 데이터 저장 및 처리 가능
    2) 또 다른 저장공간에서의 추가적인 작업 없음
  * 단점
    1) 해시 함수(Hash Function)의 성능에 전체 해시테이블의 성능 좌지우지됨
    2) 데이터의 길이가 늘어나면 그에 해당하는 저장소를 마련해 두어야 함

### 주요 용도
* 검색이 많이 필요한 경우
* 저장, 삭제, 조회 빈번한 경우
* 캐시 구현

<br><br><br>
Reference
- https://ko.wikipedia.org/wiki/%ED%95%B4%EC%8B%9C_%ED%95%A8%EC%88%98
- https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o#%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EB%8A%94-%EB%8F%84%EB%8C%80%EC%B2%B4-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C
- https://kang-james.tistory.com/entry/자료구조-해시HASH-알아보기
