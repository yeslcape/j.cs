# Tree

### 개념
하나 이상의 노드(node)로 이루어진 유한집합
<img width="518" alt="image" src="https://github.com/yeslcape/j.cs/assets/45252618/314ea981-48fc-4100-b351-32121efc2b40">

### 구성
* 하나의 루트(root) 노드
* 나머지 노드들은 n(>=0)개의 분리 집합, 자식(Child) 노드로 이루어짐

### 특징
* 트리에는 사이클이 존재X (만약 사이클이 만들어진다면, 그것은 트리가 아니고 그래프)
* 방향성이 있는 비순환 그래프
* 모든 노드는 자료형으로 표현 가능
* 루트에서 한 노드로 가는 경로는 유일한 경로
* 노드의 개수가 N개면, 간선은 N-1개

### 용어
![image](https://github.com/yeslcape/j.cs/assets/45252618/8c295871-4849-4df6-a1cd-d8ef932a071a)
* 루트 노드(root node) : 부모가 없는 노드
* 단말 노드(leaf node) : 자식이 없는 노드
* 내부 노드(internal node) : 단말 노드가 아닌 노드
* 간선(edge) : 노드를 연결 하는 선(link, branch)
* 형제(sibling) : 같은 부모를 가진 노드(형제끼린 레벨이 같음)
* 노드 크기(size) : 자신을 포함한 모든 자손 노드 개수
* 노드 깊이(depth) : 루트부터 특정 노드 까지 거쳐야하는 간선의 수
* 노드 레벨(level) : 특정 깊이를 가진 노드의 집합
* 노드 차수(degree) : 하위 트리 갯수 (A차수 : 2, E차수 :1)
* 트리 차수(degree of tree) : 트리의 최대 차수
* 트리 높이(height) : 루트 노드에서 가장 아래 있는 노드의 깊이

### 트리 순회 방식
![image](https://github.com/yeslcape/j.cs/assets/45252618/34ff0d0d-0b99-4597-b57d-de5781a369d5)
1. 전위 순회(pre-order)
* 각 부모 노드를 순차적으로 먼저 방문하는 방식이다.
  * (부모 → 왼쪽 자식 → 오른쪽 자식)
  * 1 → 2 → 4 → 8 → 9 → 5 → 10 → 11 → 3 → 6 → 13 → 7 → 14

2. 중위 순회(in-order)
* 왼쪽 하위 트리를 방문 후 부모 노드를 방문하는 방식이다.
  * (왼쪽 자식 → 부모 → 오른쪽 자식)
  * 8 → 4 → 9 → 2 → 10 → 5 → 11 → 1 → 6 → 13 → 3 →14 → 7
3. 후위 순회(post-order)
* 왼쪽 하위 트리부터 하위를 모두 방문 후 부모 노드를 방문하는 방식이다.
  * (왼쪽 자식 → 오른쪽 자식 → 부모)
  * 8 → 9 → 4 → 10 → 11 → 5 → 2 → 13 → 6 → 14 → 7 → 3 → 1
4. 레벨 순회(level-order)
* 부모 노드부터 계층 별로 방문하는 방식이다.
  * 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 13 → 14

```java
public class Tree<T> {
    private Node<T> root;

    public Tree(T rootData) {
        root = new Node<T>();
        root.data = rootData;
        root.children = new ArrayList<Node<T>>();
    }

    public static class Node<T> {
        private T data;
        private Node<T> parent;
        private List<Node<T>> children;
    }
}
```

cf) 그래프와의 차이점
그래프
- 노드와 엣지로 이루어진 네트워크 구조
- 루트 노드 없고 부모-자식 관계라는 개념 없음

<br><br><br>
Reference
- 대학자료
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Tree.md
- https://towardsdatascience.com/8-useful-tree-data-structures-worth-knowing-8532c7231e8c