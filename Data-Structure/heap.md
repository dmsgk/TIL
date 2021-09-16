# Heap





![https://blog.kakaocdn.net/dn/bm4BhE/btqCJmldPZk/56CvdNjSO51RJYnfcmzA10/img.png](https://blog.kakaocdn.net/dn/bm4BhE/btqCJmldPZk/56CvdNjSO51RJYnfcmzA10/img.png)

## 1. Heap의 개념

**최댓값과 최솟값을 빠르게 찾기 위해 고안된 자료구조**

- 트리 기반의 자료구조
- 각 노드의 key값이 해당 노드의 자식노드의 key값보다 작지 않거나 크지 않은 거의 완전한 트리
- 키 값의 대소관계는 **부모-자식 노드 사이 간에만** 성립하며 형제 노드 사이에는 영향을 미치지 않음
- i번째 노드의 자식노드가 2개인데 왼쪽 자식노드는 2i, 오른쪽 자식노드는 2i+1이고, 부모노드는 i/2가 된다.
- 쓰임
  - 우선순위 큐는 heap을 사용해 구현할 수 있다.
  - 다익스트라 알고리즘 
  - 프림 알고리즘
  - 중앙값의 근사값 구하기

## 2. Heap의 종류

- **최대 힙 (max heap)**
  - 각 노드의 키 값이 그 자식노드의 키 값보다 작지 않은 힙
  - key(T.parent(v)) ≥ key(v)
- **최소 힙 (min heap)**
  - 각 노드의 키 값이 그 자식노드의 키 값보다 크지 않은 힙
  - key(T.parent(v)) ≤ key(v)

## 3. 시간복잡도

- 새로운 원소 추가할 때 : **O(log n)**
- 힙의 원소 삭제할 때: **O(log n)**



## References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://hocheon.tistory.com/category/Algorithm/Data%20Structure
- https://gyoogle.dev/blog/computer-science/data-structure/Heap.html