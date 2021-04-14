# **BFS 너비우선 탐색**

- 너비가 넓어지는 방식으로 탐색을 하는 방법 
- **시작노드에서 부터 인접한 노드를 큐에 넣는 방법**을 사용한다.
- **BFS는 재귀로 동작하지 않는다.** 큐를 이용하여 구현하여야 한다. 

![https://blog.kakaocdn.net/dn/sp8Vd/btqHNwqK728/xrzsaZvJcLIiGJukn5G3zK/img.gif](https://blog.kakaocdn.net/dn/sp8Vd/btqHNwqK728/xrzsaZvJcLIiGJukn5G3zK/img.gif)

### BFS 구현 - in Python3

```python
def bfs(graph, start):
    visited = []
    queue = [start]

    while queue:
        n = queue.pop(0)
        if n not in visited:
            visited.append(n)
            queue += graph[n] - set(visited)
    return visited
```



- 큐의 `.append()`와 `.pop()`을 이용해 bfs를 구현하는데, pop()은 시간 복잡도가 O(N)이며, 좀 더 효율적으로 사용하고 싶으면 collections의 `deque()`를 사용하여 시간절약 가능하다.

  #### **Python의 deque 이용**

```python
from collections import deque

def bfs_dequeue(graph, start):
    visited = []
    queue = deque([start])

    while queue:
        n = queue.popleft()
        if n not in visited:
            visited.append(n)
            queue += graph[n] - set(visited)
    return visited
```



- 실제 Queue처럼 동작하는 파이썬의 `Queue` 사용

  #### **Python의 Queue()이용**

```python
from queue import Queue

def bfs_queue(graph, start):
    visited = []
    q = Queue()
    q.put(start)
    while q.qsize() > 0:
        n = q.get()
        if n not in visited:
            visited.append(n)
            for adj in graph[n]:
                q.put(adj)
    return visited
```



​	**※ 참고**

- if n not in visited 에서 visited부분은 리스트로 구현이 되어  탐색하는 시간이 O(N)이 소요된다. 
-  **visited를 딕셔너리나, set을 이용**하여 효율성을 증대
  - 기존의 딕셔너리와 set은 순서를 보존하지 않았지만 **3.7 이상부터는 딕셔너리가 순서를 보존하도록** 하여 딕셔너리({}) 사용할 것

```python
def bfs_queue(graph, start):
    visited = {}
    q = Queue()
    q.put(start)
    while q.qsize() > 0:
        n = q.get()
        if n not in visited:
            visited[n] = True
            for adj in graph[n]:
                q.put(adj)
    return list(visited.keys())
```



출력시, 리스트가 아닌 요소만 출력하고 싶다면,

```python
result = bfs_queue(adj_list,1)
print(' '.join(list(map(str, result))))
```





### References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.

- https://ebbnflow.tistory.com/234 