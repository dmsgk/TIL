# Binary Search Tree(BST, 이진탐색트리)

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/180px-Binary_search_tree.svg.png)

## Binary Search Tree 개념 및 특징

- 각 노드의 왼쪽 자식은 부모보다 작고, 오른쪽 자식은 부모보다 큰 이진트리
  - 정렬된 이진트리(sorted binary tree) 라고도 불린다.
- 중복된 노드가 없어야 함
  - 중복되는 숫자가 있을 경우 해당 노드에 count를 활용하여 세주는 것이 검색의 효율성을 향상시키는 방법임



## Binary Search Tree 핵심 연산

- 검색(search)
- 삽입(insert)
- 삭제(delete)
- 트리 생성
- 트리 삭제



## 시간 복잡도

| Algorithm  | Average      | Worst case |
| ---------- | ------------ | ---------- |
| **Space**  | **O(n)**     | **O(n)**   |
| **Search** | **O(log n)** | **O(n)**   |
| **Insert** | **O(log n)** | **O(n)**   |
| **Delete** | **O(log n)** | **O(n)**   |



- 균등 트리 : 노드 개수가 N개일 때 O(logN)
- 편향 트리 : 노드 개수가 N개일 때 O(N)
  - 편향트리(한쪽으로만 뻗음)는 연결리스트처럼 작동하여 시간복잡도가 O(N)이므로 트리를 사용할 이유가 사라짐
    - 이를 바로 잡도록 자가균형이진탐색트리(self-balancing binary search tree )를 사용한다. 
      - 자가균형이진탐색트리 : 삽입, 삭제 시 자동으로 높이를 작게 유지하는 노드기반의 이진탐색트리
    - 구체적으로는 개선된 트리가 AVL Tree, *Red-Black Tree가 있다.

> 삽입, 검색, 삭제 시간복잡도는 **트리의 Depth**에 비례



## +) 삭제의 3가지 Case

1. 자식이 없는 leaf 노드일 때 → 그냥 삭제
2. 자식이 1개인 노드일 때 → 지워진 노드에 자식을 올리기
3. 자식이 2개인 노드일 때 → 오른쪽 자식 노드에서 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값 올리기



## *Red-Black Tree

### 정의

다음의 성질을 만족하는 BST이다.

1. 각 노드는 Red 또는 Black이라는 색깔

2. Root node의 색깔은 Black

3. 각 leaf node의 색깔은 Black

4. 어떤 노드의 색깔이 red라면 두 children의 색깔은 모두 black이다.

5. 각 노드에 대해서 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은 수의 black nodes 들을 포함하고 있다. 이를 해당 노드의 `Black-Height`라고 한다. 

   *cf) Black-Height: 노드 x 로부터 노드 x 를 포함하지 않은 leaf node 까지의 simple path 상에 있는 black nodes 들의 개수*

### 삽입

우선 BST 의 특성을 유지하면서 노드를 삽입을 한다. 그리고 삽입된 노드의 색깔을 **RED 로** 지정한다. Red 로 지정하는 이유는 Black-Height 변경을 최소화하기 위함이다. 삽입 결과 RBT 의 특성 위배(violation)시 노드의 색깔을 조정하고, Black-Height 가 위배되었다면 rotation 을 통해 height 를 조정한다. 이러한 과정을 통해 RBT 의 동일한 height 에 존재하는 internal node 들의 Black-height 가 같아지게 되고 최소 경로와 최대 경로의 크기 비율이 2 미만으로 유지된다.

### 삭제

삭제도 삽입과 마찬가지로 BST 의 특성을 유지하면서 해당 노드를 삭제한다. 삭제될 노드의 child 의 개수에 따라 rotation 방법이 달라지게 된다. 그리고 만약 지워진 노드의 색깔이 Black 이라면 Black-Height 가 1 감소한 경로에 black node 가 1 개 추가되도록 rotation 하고 노드의 색깔을 조정한다. 지워진 노드의 색깔이 red 라면 Violation 이 발생하지 않으므로 RBT 가 그대로 유지된다.



## References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://en.wikipedia.org/wiki/Binary_search_tree
- https://gyoogle.dev/blog/computer-science/data-structure/Binary%20Search%20Tree.html
- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#array-vs-linked-list

