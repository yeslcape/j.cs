# Trie
![image](https://github.com/yeslcape/j.cs/assets/45252618/1464fee9-b219-4a5a-af01-abcfc18a932c)

### 개념
문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조
= 래딕스 트리(radix tree) or 접두사 트리(prefix tree) or 탐색 트리(retrieval tree)

### 특징
* 탐색 트리의 일종
* 집합에 포함된 문자열의 접두사들에 대응되는 노드들이 서로 연결된 트리
* 자동완성 기능, 사전 검색 등 문자열을 탐색하는데 특화되어있는 자료구조
  * 트리이 문자열 탐색 시간복잡도 : O(M)
  * 이진 검색 트리의 문자열 탐색 시간복잡도 : O(MlogN)
  * M : 문자열의 길이

### 작동 원리
![image](https://github.com/yeslcape/j.cs/assets/45252618/185747d6-9449-47a8-9e81-fbc7e9c9c213)
* 한 문자열에서 다음에 나오는 문자가 현재 문자의 자식 노드
* 빨간색으로 나타낸 리프 노드는 문자열의 끝

* 루트에서부터 내려가는 경로에서 만나는 글자들을 모으면, 찾고자 하는 문자열의 접두사를 찾을 수 있음

### 장점
* 빠른 문자열 검색
* 문자열을 추가하는 경우에도 문자열의 길이만큼 노드를 따라가거나 추가하면 되어, 추가와 탐색의 시간복잡도 모두 O(M)

### 단점
* 메모리 측면 비효율 (저장 공간의 크기 큼)
  * 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있음
  * 문자열이 모두 알파벳 소문자로만 이루어졌다고 해도, 1depth에 a-z까지 26개의 공간 필요
  * map이나 vector를 이용하여 필요한 노드만 메모리 할당하는 방식을 이용하기도 함

### 자료구조 구현
```java
import java.util.*;

class TrieNode {
  private Map<Character, TrieNode> childNodes = new HashMap<>();
  private boolean isLast;

  public Map<Character, TrieNode> getChildNodes() {
    return childNodes;
  }

  public boolean isLast() {
    return isLast;
  }

  public void setLast(boolean last) {
    isLast = last;
  }
}

public class Trie {
  private TrieNode rootNode;

  Trie(){
    rootNode = new TrieNode();
  }

  void insert(String word){
    TrieNode node = this.rootNode;
    for(int i=0; i<word.length(); i++) node = node.getChildNodes().computeIfAbsent(word.charAt(i), c -> new TrieNode());
    node.setLast(true);
  }

  boolean contains(String word){
    TrieNode node = this.rootNode;
    char cur;
    for(int i=0; i<word.length(); i++){
      cur = word.charAt(i);
      if(!node.getChildNodes().containsKey(cur)) return false;
      node = node.getChildNodes().get(cur);
    }
    return node.isLast();
  }

  void delete(String word){
    delete(this.rootNode, word, 0);
  }

  private void delete(TrieNode node, String word, int index){
    if(index == word.length()){
      if(!node.isLast()) throw new Error("not exist");
      node.setLast(false);
      return;
    }
    char cur = word.charAt(index);
    if(!node.getChildNodes().containsKey(cur)) throw new Error("not exist");
    TrieNode child = node.getChildNodes().get(cur);
    delete(node.getChildNodes().get(cur), word, index+1);
    if(child.getChildNodes().isEmpty()) {
      if(!child.isLast()) node.getChildNodes().remove(cur, child);
    }
  }
}
```
<b>관련 문제</b>
* [백준] 5052 전화번호 목록

<br><br><br>
Reference
- https://ko.wikipedia.org/wiki/%ED%8A%B8%EB%9D%BC%EC%9D%B4_(%EC%BB%B4%ED%93%A8%ED%8C%85)
- https://velog.io/@kimdukbae/자료구조-트라이-Trie
- https://rebro.kr/86
- https://velog.io/@cgw0519/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4