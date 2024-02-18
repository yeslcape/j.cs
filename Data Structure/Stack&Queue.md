# Stack vs Queue
|             | Stack    | Queue    |
|-------------|----------|----------|
| IN/OUT 방식   | LIFO     | FIFO     |

## Stack
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmlHbt%2FbtrnjHxkal4%2FMCvYE5QEcgfbtZhXM0cJb0%2Fimg.png)
> 스택(Stack) : "쌓다" 라는 의미로, 데이터를 차곡차곡 쌓아 올린 형태의 자료구조

### 특징
* LIFO(Last In First Out) : 후입선출 - 가장 마지막에 삽입된 데이터가 가장 먼저 삭제됨
* 같은 구조와 크기의 데이터를 정해진 방향으로만 쌓을 수 있음

### 연산자
* top : 가장 마지막 삽입/가장 먼저 나갈 데이터 확인
* push : 데이터 넣기
* pop : 최상위 데이터 빼기

### 활용 예시
* 웹 브라우저 방문기록 (뒤로가기) : 가장 나중에 열린 페이지부터 다시 보여줌
* 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력
* 실행 취소 (undo) : 가장 나중에 실행된 것부터 실행 취소
* 후위 표기법 계산
* 수식의 괄호 검사 : 연산자 우선순위 표현을 위한 괄호 검사

### 구현 1. 배열
```
/* 스택 포인터 : 다음 값이 들어갈 위치 가리키기 */
private int sp = -1;

/* push : 데이터 넣기 */
public void push(Object o) {
    if (isFull(o)) return;
    
    stack[++sp] = o;
}

/* pop : 데이터 빼기 */
public Object pop() {
    if (isEmpty(sp)) return null; 
    
    Object o = stack[sp--];
    return o;
}

/* top : 데이터 확인 */
public Object top() {
    if (isEmpty(sp)) return null;
    
    Object o = stack[sp];
    return o;
}
```

### 구현 2. 연결리스트
```
/* Node 선언 */
public class Node {
    public int data;
    public Node next;
    
    public Node() {}
    
    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

/* 스택 구현 */
public class Stack {
    private Node head;
    private Node top;

    /* 스택 초기화 */
    public Stack() {
        head = top = null;
    }

    /* 노드 생성 */
    private Node createNode(int data) {
        return new Node(data);
    }

    /* 비었는지 여부 확인 */
    private boolean isEmpty() {
        return top == null ? true : false;
    }

    /* push : 데이터 넣기 */
    public void push(int data) {
        if (isEmpty()) { // 스택이 비어있다면
            head = createNode(data);
            top = head;
        }
        else { //스택이 비어있지 않다면 마지막 위치를 찾아 새 노드를 연결시킨다.
            Node pointer = head;

            while (pointer.next != null)
                pointer = pointer.next;

            pointer.next = createNode(data);
            top = pointer.next;
        }
    }

    /* pop : 데이터 빼기 */
    public int pop() {
        int popData;
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            popData = top.data; // pop될 데이터를 미리 받아놓는다.
            Node pointer = head; // 현재 위치를 확인할 임시 노드 포인터

            if (head == top) // 데이터가 하나라면
                head = top = null;
            else { // 데이터가 2개 이상이라면
                while (pointer.next != top) // top을 가리키는 노드를 찾는다.
                    pointer = pointer.next;

                pointer.next = null; // 마지막 노드의 연결을 끊는다.
                top = pointer; // top을 이동시킨다.
            }
            return popData;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.
    }

    /* top : 현재 데이터 확인 */
    public int top() {
        if (!isEmpty()) { // 스택이 비어있지 않다면!! => 데이터가 있다면!!
            return top.data;
        }
        return -1; // -1은 데이터가 없다는 의미로 지정해둠.
    }
}
```

## Queue
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FboPAln%2FbtrnfBrlYFt%2FNRNKLJXH4DqqZgi2ieqhZ0%2Fimg.png)
> 큐(Queue) : "표를 사러 일렬로 늘어선 사람들로 이루어진 줄"을 의미하며, 먼저 들어온 순으로 먼저 나가는 자료구조

### 특징 
* FIFO(First In First Out) : 선입선출 - 먼저 들어온 게 먼저 삭제됨
* 삽입, 삭제가 다른 방향에서 이루어짐

### 연산자
* enQueue : 데이터 넣기
* deQueue : 데이터 빼기
* front : 가장 첫 원소 확인 (deQueue 위치 확인)
* rear : 가장 끝 원소 확인 (enQueue 위치 확인)

### 활용 예시
* 프로세스 관리
* 너비 우선 탐색(BFS)
* 캐시(Cache)

### 큐 개선
* 일반 큐
  * 단점 : 큐에 빈 메모리가 남아 있어도, 꽉 차 있는 것으로 판단 가능 = rear가 끝에 도달했을 경우
  * 개선 : 원형 큐
* 원형 큐 : 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주
  * 초기 공백 상태일 때 front와 rear = 0
  * 단점 : 메모리 공간은 잘 활용하지만, 배열로 구현되어 있어 큐의 크기 제한
  * 개선 : 연결리스트 큐
* 연결리스트 큐 : 크기 제한 없고, 삽입 삭제 편리
  * 삽입/삭제를 스택처럼 O(1)에 가능

### 구현. 원형 큐
```
private int size = 0; 
private int rear = 0; 
private int front = 0;

Queue(int size) { 
    this.size = size;
    this.queue = new Object[size];
}

/* enqueue : 데이터 넣기 */
public void enqueue(E item) {
    Node oldlast = tail; // 기존의 tail 임시 저장
    tail = new Node; // 새로운 tail 생성
    tail.item = item;
    tail.next = null;
    if(isEmpty()) head = tail; // 큐가 비어있으면 head와 tail 모두 같은 노드 가리킴
    else oldlast.next = tail; // 비어있지 않으면 기존 tail의 next = 새로운 tail로 설정
}

/* dequeue : 데이터 빼기 */
public T dequeue() {
    // 비어있으면
    if(isEmpty()) {
        tail = head;
        return null;
    }
    // 비어있지 않으면
    else {
        T item = head.item; // 빼낼 현재 front 값 저장
        head = head.next; // front를 다음 노드로 설정
        return item;
    }
}
```

reference
- https://devuna.tistory.com/22
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Stack%20%26%20Queue.md
