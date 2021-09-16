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
    - 구체적으로는 개선된 트리가 AVL Tree, RedBlack Tree가 있다.

> 삽입, 검색, 삭제 시간복잡도는 **트리의 Depth**에 비례



## +) 삭제의 3가지 Case

1. 자식이 없는 leaf 노드일 때 → 그냥 삭제
2. 자식이 1개인 노드일 때 → 지워진 노드에 자식을 올리기
3. 자식이 2개인 노드일 때 → 오른쪽 자식 노드에서 가장 작은 값 or 왼쪽 자식 노드에서 가장 큰 값 올리기



## References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://en.wikipedia.org/wiki/Binary_search_tree
- https://gyoogle.dev/blog/computer-science/data-structure/Binary%20Search%20Tree.html

