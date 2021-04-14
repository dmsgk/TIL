# Graph

- 그래프란 객체의 일부 쌍(pair)들이 연관되어 있는 객체 집합 구조를 의미한다.

**오일러 경로**

- 오일러의 정리
  - 모든 정점이 짝수 개의 차수를 갖는다면 한붓그리기 가능함
- 오일러 경로: 모든 간선을 한 번씩 방문하는 유한 그래프

**해밀턴 경로**

- 해밀턴 경로: 각 정점을 한 번씩 방문하는 무향 또는 유향 그래프 경로

- 해밀턴 순환: 원래의 출발점으로 돌아오는 경로

  - 이 중에서 최단 거리를 찾는 문제는 **외판원문제(TSP)**로 유명하다.

    - 외판원문제는 dp로 최적화가 가능하다.

      

## Graph Search

- 그래프 순회란 그래프의 각 정점을 방문하는 과정을 의미한다.

- 크게 깊이우선탐색(DFS)과 너비우선탐색(BFS)로 구분된다.

  

## 파이썬에서의 그래프 구현

- 파이썬에서 그래프는 **인접리스트**나 **인접행렬**으로 구현할 수 있음
- 노드의 개수에 비해 간선(엣지)의 개수가 훨씬 적다면, 인접행렬보단 인접리스트를 사용하는 것이 탐색에 효율적
  -  연결된 노드의 수만큼만 살펴보면 되고 메모리도 간선 수만큼만 차지하기 때문.
- 두 노드의 연결 관계를 알고싶다면 인접 행렬이 효율적임

### 1. **인접리스트(Adjacency list)**

![img](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f89d1b82-25f9-42ba-b7ae-367b249269c7/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20210414%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20210414T062333Z&X-Amz-Expires=86400&X-Amz-Signature=2821145fe43b5e454f6c440904dd5543d4013a9c4c5659096d952be4af7ca2ba&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22)

- 파이썬의 `set`타입 이용하여 인접리스트를 구현한다.

```python
adj_list = {1: set([2,3]),
        2: set([1,4,5]),
        3: set([1]),
        4: set([2]),
        5: set([2])}
```

- set 내부 원소는 다양한 값을 함께 가질 수 있지만, mutable 한 값은 가질 수 없음.
  -  immutable에는 Number, String, Tuple이 있고 mutable에는 List, Dictionary가 있음

### 2. **인접행렬(Adjacency matrix)**

![img](https://blog.kakaocdn.net/dn/xwRMC/btqHJozSnRY/H7LnYSu4fdHYevS3dwDnt1/img.png)

이를 파이썬 인접행렬로 표현하면 다음과 같다. 

```python
s = [[0]*6 for i in range(6)]
s[1][2] = 1
s[2][1] = 1
s[1][3] = 1
s[3][1] = 1
s[2][4] = 1
s[4][2] = 1
s[2][5] = 1
s[5][2] = 1
```





### References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://ebbnflow.tistory.com/234 