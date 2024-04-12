# B+Tree
<img width="809" alt="스크린샷 2024-04-13 오전 7 46 08" src="https://github.com/yeslcape/schedule/assets/45252618/c99fbfaf-d12c-4cab-8fc0-4749a50eb3d1">

![image](https://github.com/yeslcape/schedule/assets/45252618/2b1c7369-e2ce-4bf2-a71b-6149ab10235f)

### 개념
- 데이터베이스 index에 자주 사용되는 자료구조
- B-Tree 계열의 Balanced Tree 종류 중 하나

### B-Tree 단점
B-Tree는 탐색을 위해서 노드를 찾아서 이동해야함

### 특징
- 같은 레벨의 모든 키값들 정렬
- 같은 레벨의 형제 노드들 연결리스트 형태
  - 형제 노드들끼리도 조회 가능
  - 범위 검색 성능이 좋음
- 리프노드의 부모 key는 리프노드의 첫번째 key보다 작거나 같음
- internal 노드에는 키만 저장
  - 이 키를 사용해서 자식 노드의 메모리 상 위치 판단
  - 데이터의 포인터 없음
  - 데이터를 찾기 위한 포인터도 리프 노드에만
  - internal 노드의 크기를 줄여 메모리 사용이 효율적
- 새로운 데이터의 삽입 및 삭제 비교적 간단 
  - 삽입 : 리프 노드에 새로운 데이터 추가
  - 삭제 : 데이터를 제거하면서 B+Tree의 균형 유지

### M차 B+Tree 특징 (=B-Tree)
- 노드는 최대 M개 부터 M/2개 까지의 자식 가질 수 있음
- 노드에는 최대 M−1개 부터 [M/2]−1개의 키 포함될 수 있음
- 노드의 키가 x개라면 자식의 수는 x+1개
- 최소차수는 자식수의 하한값을 의미하며, 최소차수가 t라면 M=2t−1을 만족 (최소차수 t가 2라면 3차 B트리이며, key의 하한은 1개)

### 검색
- B-Tree와 동일하므로 생략

### 삽입
1. 분할이 일어나지 않고, 삽입 위치가 리프노드의 가장 앞 key 자리가 아닌 경우
   - B트리와 똑같은 삽입 과정 수행
2. 분할이 일어나지 않고, 삽입 위치가 리프노드의 가장 앞 key 자리인 경우
   - 삽입 후 부모 key를 삽입된 key로 갱신하고, data 넣기
   ![image](https://github.com/yeslcape/schedule/assets/45252618/339227f4-0601-4297-a654-8956021a3ab9)
3. 분할이 일어나는 삽입과정 
    - 분할이 일어나는 노드가 리프노드가 아니라면 기존 B트리와 똑같이 분할을 진행합니다. 중간 key를 부모 key로 올리고, 분할한 두개의 노드를 왼쪽, 오른쪽 자식으로 설정 
    - 분할이 일어나는 노드가 리프노드라면 중간 key를 부모 key로 올리지만, 오른쪽 노드에 중간 key를 포함하여 분할합니다. 또한 리프노드는 연결리스트이기 때문에 왼쪽 자식노드와 오른쪽 자식 노드를 이어줘 연결리스트 형태 유지
    ![image](https://github.com/yeslcape/schedule/assets/45252618/b26eb727-c81b-4d67-b6f1-d613036aa797)

### 삭제
1. 삭제할 key k가 index에 없고, 리프노드의 가장 처음 key가 k가 아닌 경우 
    - B트리 삭제과정과 동일
2. 삭제할 key k가 리프노드의 가장 처음 key인 경우
    - 삭제할 key k가 리프노드의 가장 처음 key인 경우에는 항상 k가 index 내에 존재한다고 가정
    - 먼저 리프노드의 k를 삭제하는 과정을 수행
      - key의 개수가 최소 key의 개수라면 B트리의 삭제 과정 중 형제노드의 key를 빌려오는 경우나 부모key와 병합하는 등 과정들 동일하게 수행. 단, 리프노드가 병합할 때는 부모key와 오른쪽 자식의 처음 key가 동일하기 때문에 부모key를 가져오는 과정만 생략하고 왼쪽 자식과 오른쪽 자식을 병합만
    - 리프노드의 k를 삭제한 후, index내의 k를 inorder successor로 변경
      ![image](https://github.com/yeslcape/schedule/assets/45252618/d340e30e-9e61-48e2-b0f0-3493925f150b)

### B-Tree와의 차이점
- 검색
  - 데이터를 검색할 때 항상 리프 노드까지 이동하므로 검색 경로가 단순해진다. 
  - B-Tree: 모든 노드(internal node + leaf node)에 키와 값이 함께 저장 
  - B+Tree: internal 노드에는 키만 저장, 리프 노드에는 키와 값 저장
- 포인터의 사용
  - B-Tree: internal 노드의 포인터를 통해서만 리프 노드로 이동 가능
    - 추가적인 단계 필요 (단점)
  - B+Tree: 리프 노드끼리 서로 연결 리스트로 연결되어 있음
    - internal 노드를 통하지 않고도 형제 노드로 이동 가능하고, 범위 검색이나 범위 쿼리가 쉽다.
- 범위 쿼리와 범위 검색 
  - B-Tree: 범위 쿼리를 수행하려면 트리의 루트에서부터 리프 노드까지 이동하면서, 루트 노드, internal 노드에 있는 데이터까지 함께 조회
  - B+Tree: 데이터는 리프 노드에만 존재하므로, 범위 쿼리는 리프 노드를 시작으로 연결된 리스트를 따라가면 모든 데이터 조회 가능
- 순차 탐색 및 정렬 
  - B-Tree: 순차적인 탐색이나 정렬을 위한 추가적인 알고리즘이 필요해서 (예. inorder traversal) B+Tree보다 더 복잡 
  - B+Tree: 연결된 리스트를 따라가면서 순차 탐색이 용이하며, 키들은 항상 정렬된 상태를 유지하면서 저장
- 메모리 사용 
  - B-Tree: 리프 노드와 내부 노드가 각각 데이터와 포인터까지 가지고 있기 때문에 B+Tree보다 더 많은 메모리 공간 차지 
  - B+Tree: 데이터는 리프 노드에만 저장되고, internal 노드는 키만 갖고 있으면 되므로, 메모리 효율이 좋다.

### 주요 사용
- MySQL의 InnoDB 스토리지 엔진
- 데이터베이스 인덱스와 파일 시스템 사용에 적합
- 리프 노드를 제외하고 데이터를 담아두지 않기 때문에 internal 노드의 경우, 한정된 메모리 안에 더 많은 key들을 수용할 수 있다. 즉, 하나의 노드에 더 많은 key들을 저장하기 때문에 동일한 데이터 개수라면, 트리의 높이는 더 낮아진다. 
- cache hit를 높일 수 있을 뿐만 아니라, 범위 검색이나 범위 쿼리에도 큰 강점을 갖고 있으며, 상대적으로 굉장히 느린 secondary storage에 대한 접근 횟수가 현저히 줄어든다. 
- 테이블 풀 스캔 시, B-Tree의 경우에는 데이터가 internal 노드와 리프 노드에 퍼져있기 때문에 모든 노드를 탐색해야 한다. B+tree는 리프 노드에만 데이터가 존재하고, 존재하는 모든 데이터는 리프 노드에 있기 때문에 한 번의 선형탐색만 하면 되므로 매우 빠르다.
- DB 인덱스로 해시 테이블 사용할 수 없는 이유 : 모든 값이 정렬되어있지 않으므로, 해시 테이블에서는 특정 기준보다 크거나 작은 값을 찾을 수 없다.
- RedBlack-Tree가 아니라 B+Tree인 이유 : RedBlack-Tree는 무조건 하나의 노드에 하나의 데이터 요소만을, B+Tree는 하나의 노드에 여러 개의 데이터 요소를 저장
![image](https://github.com/yeslcape/schedule/assets/45252618/54a9c07c-6c29-40de-83f2-ae98b45594b0)

### B+Tree 시각화 사이트
https://www.cs.usfca.edu/~galles/visualization/BPlusTree.html

<br><br><br>
Reference
- https://www.geeksforgeeks.org/introduction-of-b-tree/
- https://engineerinsight.tistory.com/336
- https://velog.io/@emplam27/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-B-Plus-Tree