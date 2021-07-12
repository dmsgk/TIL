# Topology Sort (위상정렬)

## 개념

- 방향이 있는 유향그래프의 방향을 거스르지 않도록 나열하는 방식을 의미한다.
- 위상정렬이 성립하기 위해서는 그래프의 순환이 존재하지 않아야 한다. 



## 수행과정

- 자기 자신을 가르키지 않는 노드를 찾는다.
- 찾은 노드를 출력하고 출력한 노드와 해당 노드에서 출발하는 경로를 제거한다. 
- 노드가 남아있지 않을 때까지 해당 과정을 반복한다.



## 시간복잡도

O(V+E)로 매우 효율적인 알고리즘이라고 할 수 있다. 



## 관련 문제

백준 2252번 줄세우기

```python
# 내 풀이
import sys
from collections import deque, defaultdict

n, m = map(int, sys.stdin.readline().rstrip().split())

graph = defaultdict(set)
indegree = {i : 0 for i in range(1, n+1)}
queue = deque()
ans = []

for _ in range(m):
    a, b = map(int, sys.stdin.readline().rstrip().split())
    graph[a].add(b)
    indegree[b] += 1

for k, v in indegree.items():
    if v == 0:
        queue.append(k)

        
while queue:
    q = queue.popleft()
    ans.append(q)
    for c in graph[q]:
        indegree[c] -= 1
        if indegree[c] == 0:
            queue.append(c)
    del graph[q]

print(" ".join(map(str, ans)))
```



## References

- https://ko.wikipedia.org/wiki/%EC%9C%84%EC%83%81%EC%A0%95%EB%A0%AC