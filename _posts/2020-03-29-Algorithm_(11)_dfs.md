---
title: "Algorithm - (11) DFS"
published: false
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
<!--link: -->
---

## DFS (Depth-First Search)
> * 대표적인 그래프 **탐색** 알고리즘  
>	- 너비 우선 탐색 (Breadth First Search): 정점들과 같은 레벨에 있는 노드들 (형제 노드들)을 먼저 탐색하는 방식  
>	- **깊이 우선 탐색 (Depth First Search)**: 정점의 자식들을 먼저 탐색하는 방식  


<center>
	<a href="https://en.wikipedia.org/wiki/Depth-first_search">
		<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Depth-first-tree.svg/450px-Depth-first-tree.svg.png"/>
	</a>
</center>


## DFS 알고리즘 구현
- 자료구조 스택과 큐를 활용함  
	- need_visit **!!스택!!**과 visited 큐, 두 개의 자료 구조를 생성  
​
> BFS 자료구조는 두 개의 큐를 활용하는데 반해, DFS 는 스택과 큐를 활용한다는 차이가 있음을 인지해야 함  

## DFS 시간 복잡도
- 일반적인 DFS 시간 복잡도  
	- 노드 수: V  
	- 간선 수: E    
	- 시간 복잡도: O(V + E)  
  
## C++
```cpp

```


## Python
* 파이썬에서 제공하는 딕셔너리와 리스트 자료 구조를 활용해서 그래프를 표현할 수 있음
```python
graph = dict()

graph['A'] = ['B', 'C']
graph['B'] = ['A', 'D']
graph['C'] = ['A', 'G', 'H', 'I']
graph['D'] = ['B', 'E', 'F']
graph['E'] = ['D']
graph['F'] = ['D']
graph['G'] = ['C']
graph['H'] = ['C']
graph['I'] = ['C', 'J']
graph['J'] = ['I']
```
​
```python
def dfs(graph, start_node):
    visited, need_visit = list(), list()
    need_visit.append(start_node)
    
    while need_visit:
        node = need_visit.pop()  #맨 끝데이터 
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])
    
    return visited
```

