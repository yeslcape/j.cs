# Heap

### 개념
최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전이진트리(complete binary tree)를 기본으로 한 자료구조(tree-based structure)
![image](https://github.com/yeslcape/j.cs/assets/45252618/5e3fd7b0-f76b-4197-97fe-e464b9c0ba5b)

### 구성
![image](https://github.com/yeslcape/j.cs/assets/45252618/a9bb364e-3b3b-424a-b892-c132195db4da)

부모 노드의 인덱스는 1로, 왼쪽 자식 노드부터 2, 3 순서
- (부모 노드의 인덱스) = (자식 노드 인덱스) / 2
- (왼쪽 자식 노드의 인덱스) = (부모 노드의 인덱스) * 2
- (오른쪽 자식 노드의 인덱스) = (부모 노드의 인덱스) * 2 + 1

### 특징
* 부모 노드가 가진 값은 자식 노드의 값보다 무조건 크거나(Max Heap) 작아야(Min Heap) 함
* 완전 이진 트리이므로 배열을 통해 구현 가능
* 가장 크거나 작은 값을 찾아내는 연산을 빠르게 하기위해 고안된 자료구조 : O(logn)
* 반정렬 상태
* 힙 트리는 중복된 값 허용 (이진 탐색 트리는 중복값 허용X)

### 힙 vs 이진 탐색 트리
![image](https://github.com/yeslcape/j.cs/assets/45252618/ab084e20-f31a-48cd-9dbb-d796fb777c0c)

* 공통점
  * 모두 완전 이진 트리이다.

* 차이점
  * (최대힙의 경우) 힙은 각 노드의 값이 자식 노드보다 크거나 같다.
  * 이진 탐색 트리는 각 노드의 왼쪽 자식은 더 작은 값으로, 오른쪽 자식은 더 큰 값으로 이루어져있다. (왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드)
  * 힙은 최대/최소 검색을, 이진 탐색 트리는 탐색을 위한 구조이다.

### 자료 추가
- 트리의 높이만큼 비교 : O(logN)
1. 새로운 노드를 트리의 맨 뒤에 추가한다. (완전 이진 트리의 형태를 깨면 안됨)
2. 추가된 노드와 부모 노드를 비교하여 자식 노드가 크다면 서로의 위치를 바꾼다.
3. 2번 작업을 부모 노드가 더 클때까지 반복한다.

### 자료 삭제 (O(logN))
- 트리의 높이만큼 비교 : O(logN)
1. 맨 뒤에있는 노드를 Root자리로 옮긴다.
2. 자식 노드중 값이 더 큰 노드와 비교하여 자식 노드가 값이 더 크다면 위치를 바꾼다.
3. 2번의 작업을 자식노드보다 자신이 클때까지 반복한다.
<br><br><br>
Reference
- https://ko.wikipedia.org/wiki/%ED%9E%99_(%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0)
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Heap.md
- https://velog.io/@gnwjd309/data-structure-heap