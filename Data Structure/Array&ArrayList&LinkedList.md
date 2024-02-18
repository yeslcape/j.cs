# Array vs ArrayList vs LinkedList
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbxSQdR%2FbtqTyBzXfTx%2FJg0RdLWPPDZhnPv2ywDZ3k%2Fimg.png)

## Array vs ArrayList vs LinkedList 특징
|             | Array    | ArrayList | LinkedList   |
|-------------|----------|-----------|--------------|
| 사이즈         | 불변       | 가변        | 가변           |
| 조회          | 빠름(O(1)) | 빠름(O(1))  | 느림(O(N))     |
| (비순차적) 삽입   | 느림(O(N)) | 느림(O(N))  | 빠름(O(1))     |
| (비순차적) 삭제   | 느림(O(N)) | 느림(O(N))  | 빠름(O(1))     |
| List 크기 구하기 | O(N) | O(N)  | O(1) or O(N) |

## Array
> 데이터타입 배열이름[배열길이]

```
int arr[10];
String arr[5];
```

### 특징
* 배열을 선언함과 동시에 데이터 타입과 길이 결정
* 메모리 공간에 할당할 사이즈를 미리 정해놓고 사용하는 자료구조

### 장점
* 인덱스를 통해 원하는 값을 빠르게 검색 가능
* 순차적인 데이터 추가/삭제 빠름

### 단점
* 길이를 가변적으로 변경해야할 필요가 있을 경우 사용 불가
* 데이터 최대 수를 알지 못할 경우 사용 불가
* 중간에 데이터 삽입/삭제 시 비효율적 - 원래값을 뒤로 밀어내고 해당 index에 덮어씌워야 한다.

## ArrayList
```
import java.util.ArrayList;

ArrayList list = new ArrayList(); // 타입 미설정, Object로 선언
ArrayList<Member> members = new ArrayList<Member>(); // 타입 설정, Member 객체만 사용 가능
ArrayList<Integer> num = new ArrayList<Integer>(); // 타입 설정, int 타입
ArrayList<Integer> num2 = new ArrayList<>(); // new에서 타입 생략 가능, int 타입
ArrayList<Integer> num3 = new ArrayList<Integer>(10); // 초기 용량(capacity) 지정
ArrayList<Integer> list2 = new ArrayList<Integer>(Arrays.asList(1,2,3)); // 생성 시 값 추가
```

### 특징
* 내부적으로 데이터를 배열에서 관리
* 배열에 더 이상 저장할 공간이 없으면 자체적으로 배열의 크기를 늘려 처리

### 장점
* 인덱스를 통해 원하는 값 빠르게 검색 가능
* 가변적으로 데이터 추가 삭제 가능

### 단점
* 데이터 추가/삭제 시 시간 오래 걸림

## LinkedList
```
class Node {
    int data;
    Node* next;
}
```

### 특징
* 불연속적으로 저장된 데이터를 서로 연결(link)한 형태로 구성되어있는 자료구조

### 장점
* 노드를 추가하거나 삭제하는 방식으로 구조를 변경 가능

### 단점
* 데이터 조회 시 처음부터 순차적으로 검색 필요
