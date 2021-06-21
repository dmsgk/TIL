# Dijikstra's Algorithm

## Dijikstra's Algorithm

- 그리디 알고리즘의 한 종류
- 이 알고리즘은 변형이 많다. 다익스트라의 원래 알고리즘은 두 꼭짓점 간의 가장 짧은 경로를 찾는 알고리즘이지만, 더 일반적인 변형은 한 꼭짓점을 "소스" 꼭짓점으로 고정하고 그래프의 다른 모든 꼭짓점까지의 최단경로를 찾는 알고리즘으로 최단 경로 트리를 만드는 것이다.



## 시간복잡도

- 최초 구현 시에는 시간복잡도 O(V^2)
- BFS 시 가장 가까운 순서를 찾을 때 우선순위 큐를 적용하는 경우 O((V+E) log V)
- 모든 정점이 출발지에서 도달이 가능하다면 최종적으로 O(E log V) 

### References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%81%AC%EC%8A%A4%ED%8A%B8%EB%9D%BC_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98

