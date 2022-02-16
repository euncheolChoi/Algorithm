**[DFS, BFS 알고리즘(1)]<https://mosobamboo-dev.tistory.com/30>**  
**[DFS, BFS 알고리즘(2)]<https://mosobamboo-dev.tistory.com/31>**

#### 1) 재귀함수 구조
```
# 가장 간단한 재귀 함수 예시

def recursive_function():
	print('재귀 함수를 호출합니다')
    recursive_function()

recursive_function() # 문자열을 무한히 출력. 재귀의 최대 깊이를 초과했다는 오류 메세지가 뜬다. 

# 재귀 함수의 종료조건을 설정한 경우
def recursive_function(i):
	# 100번째 출력했을 때 종료되도록 종료 조건 명시
    if i == 100:
    	return 
    print(i, '번째 재귀 함수에서', i + 1, '번째 재귀 함수를 호출합니다.' )
    recursive_function(i + 1 ) 
    print(i, '번째 재귀 함수를 종료합니다.' )

recursive_funtion(1)
```

#### 2) DFS 알고리즘
```
# DFS는 스택을 이용하는 알고리즘이기 때문에 실제 구현은 재귀 함수를 이용했을 때 매우 간결하게 구현할 수 있다.

#DFS 메서드 정의 

def dfs(graph, v, visited):
	# 현재 노드를 방문 처리
    visited[v] = True
    print(v, end=' ')
    # 현재 노드와 연결된 다른 노드를 재귀적으로 방문
    for i in graph[v]:
    	if not visited[i]:  # if not구문은 조건이 발생하지 않았는지를 판단한다. 조건이 False이면 구문이 실행된다.
        	dfs(graph, i, visited)
            
# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트)
# 첫 번째 노드의 숫자는 관례적으로 1이므로 이중 리스트의 0번째 인덱스는 제외해놓는다. 
graph = [
	[],
    [2, 3, 8],
    [1, 7],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

```

#### 3) BFS 알고리즘

```
from collections import deque

# BFS 메서드 정의 
def bfs(graph, start, visited):
	#큐 구현을 위해 deque 라이브러리 사용
    queue = deque([start])
    # 현재 노드를 방문 처리
    visited[start] = True
    # 큐가 빌 때까지 반복 
    while queue:
    	# 큐에서 하나의 원소를 뽑아 출력
        v = queue.popleft()
        print(v, end='')
        # 해당 원소와 연결된, 아직 방문하지 않은 원소들을 큐에 삽입
        for i in graph[v]:
        	if not visited[i]:
            queue.append(i)
            visited[i] = True

# 각 노드가 연결된 정보를 리스트 자료형으로 표현(2차원 리스트) 
graph = [
	[],
    [2, 3, 8],
    [1, 4, 5],
    [3, 5],
    [3, 4],
    [7],
    [2, 6, 8],
    [1, 7]
]

# 각 노드가 방문된 정보를 리스트 자료형으로 표현(1차원 리스트) 
visited = [False] * 9

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)
```
#### 4) page.149 음료수 얼려 먹기

```
n, m = map(int, input().split())

# 2차원 리스트의 맵 정보 입력받기
graph = []
for i in range(n):
  graph.append(list(map(int, input())))

#dfs로 특정한 노드를 방문한 뒤에 연결된 모든 노드들도 방문
def dfs(x,y):
  # 주어진 범위를 벗어나는 경우에는 즉시 종료
  if x<=-1 or x>=n or y <=-1 or y >= m:
    return False
  # 현재 노드를 아직 방문하지 않았다면
  if graph[x][y] == 0:
    # 해당 노드 방문 처리
    graph[x][y] = 1
    # 상하좌우의 위치도 모두 재귀적으로 호출
    dfs(x-1, y)
    dfs(x+1, y)
    dfs(x, y-1)
    dfs(x, y+1)
    return True

  return False

#모든 노드(위치)에 대하여 음료수 채우기
result = 0
for i in range(n):
  for j in range(m):
    # 현재 위치에서 dfs수행
    if dfs[i][j] == True:
      result += 1
print(result)
```


