# DFS 깊이우선탐색

시작 노드에서부터 가장 깊이가 깊은 곳까지 방문 후 이전 위치로 돌아와 가장 깊은 노드까지 방문하는 탐색법

![https://blog.kakaocdn.net/dn/bLD5Dt/btqHVokzUO9/cwQ6X4Z7rRi2ODtCwvbdqK/img.gif](https://blog.kakaocdn.net/dn/bLD5Dt/btqHVokzUO9/cwQ6X4Z7rRi2ODtCwvbdqK/img.gif)

## 구현방법

- 스택을 이용하는 방법

  ```python
  def dfs_iteration(graph, root):
      # visited = 방문한 꼭지점들을 기록한 리스트
      visited = []
      # dfs는 stack, bfs는 queue개념을 이용한다.
      stack = [root]
      
      while(stack): #스택에 남은것이 없을 때까지 반복
          node = stack.pop() # node : 현재 방문하고 있는 꼭지점
          
          #현재 node가 방문한 적 없다 -> visited에 추가한다.
          #그리고 해당 node의 자식 node들을 stack에 추가한다.
          if(node not in visited):
              visited.append(node)
              stack.extend(graph[node])
      return visited
  ```

- 재귀를 이용하는 방법

  ```python
  def dfs(graph, start, visited=[]):
      visited.append(start) ## ★★★★★
      
      for node in graph[start]:
          if node not in visited:
              dfs_recursive(graph, node, visited) ## ★★★★★
      
      return visited
  ```

  



#### References

- https://ebbnflow.tistory.com/234 [Dev Log : 삶은 확률의 구름]

- https://juhee-maeng.tistory.com/25 [BIU]