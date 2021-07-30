# MST(Minimum-Spanning-Tree)

## Spanning-Tree

- = 신장트리 = 스패닝트리
- 그래프의 모든 정점을 포함하는 트리
- 그래프의 최소 연결 부분 그래프 이다. n개의 정점을 가지는 그래프의 최소 간선의 수는 (n-1)개이고, (n-1)개의 간선으로 연결되어 있으면 필연적으로 트리 형태가 되고 이것이 바로 Spanning Tree가 된다.



## MST(Minimum-Spanning-Tree)

### MST 개념

- Spanning Tree 중에서 가중치가 가장 작은 트리
- 즉, 네트워크(가중치를 간선에 할당한 그래프)에 있는 모든 정점들을 가장 적은 수의 간선과 비용으로 연결

### MST의 특징

- 간선의 가중치의 합이 최소여야 한다.
- n개의 정점을 가지는 그래프에 대해 반드시 (n-1)개의 간선만을 사용해야 한다.
- 사이클이 포함되어서는 안된다.



### MST 구현방법

#### 1. Kruskal MST 알고리즘

탐욕적인 방법(greedy method) 을 이용하여 네트워크(가중치를 간선에 할당한 그래프)의 모든 정점을 최소 비용으로 연결하는 최적 해답을 구하는 것

#### 2. Prim MST 알고리즘





## References

- https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html

