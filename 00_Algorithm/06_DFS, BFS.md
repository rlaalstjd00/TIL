## 그래프의 탐색

#### DFS : 깊이 우선 탐색

- 모든 노드를 한번씩 방문해 최대한 깊이 많이 가는 것

- 스택 이용해서 갈 수 있는 만큼 최대한 많이 가고 거친 곳을 스택에 저장

- 더이상 방문할 노드가 없다면 이전 정점으로 돌아간다.

- `check` 배열을 만들어 방문한 노드와 아닌 노드를 구분함

  ```` python
  def dfs(v):
      check[v] = False
  
      print(v, end= ' ')
  
      for i in edge[v]:
          if check[i] == True:
              dfs(i)
  ````
  

#### BFS : 너비 우선 탐색

- 모든 노드를 한번씩 방문해 최대한 넓게 가는 것

- 큐나 덱 사용

  ```` python
  def bfs(v):
      d = deque()
      d.append(v)
      
      check[v] = True
  
      while d:
          v = d.popleft()
          print(v, end=' ')
          for i in edge[v]:
              if check[i] == False:
                  d.append(i)
                  check[i] = True
  ````

#### DFS와 BFS의 비교

- 단순히 그래프의 모든 정점을 방문하는 문제
  - 아무거나 사용해도 상관없음
- 경로의 특징을 저장해야하는 문제
  - DFS 사용 (BFS는 경로의 특징을 가지지 못함)
- 최단거리 구하는 문제
  - BFS 사용 
