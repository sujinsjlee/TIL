---
title: "Algorithm - (10) BFS"
published: false
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
<!--link: -->
---

## BFS (Breadth-First Search)   
* 대표적인 그래프 **탐색** 알고리즘  
- 너비 우선 탐색 (Breadth First Search): 정점들과 같은 레벨에 있는 노드들 (형제 노드들)을 먼저 탐색하는 방식  
- 깊이 우선 탐색 (Depth First Search): 정점의 자식들을 먼저 탐색하는 방식  

<center>
	<a href="https://en.wikipedia.org/wiki/Breadth-first_search">
		<img src="https://upload.wikimedia.org/wikipedia/commons/4/46/Animated_BFS.gif"/>
	</a>
</center>

## BFS 알고리즘 구현
- 자료구조 큐를 활용함  
	- need_visit 큐와 visited 큐, 두 개의 큐를 생성  

## 시간 복잡도
- 일반적인 BFS 시간 복잡도  
	- 노드 수: V  
	- 간선 수: E  
	- 시간 복잡도: **O(V + E)**  

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

* pop(), extend() 함수
```python
data = [1, 2, 3]
data.pop() #뒤 데이터 삭제
data.pop(0) #pop(index) index데이터 삭제
data.extend([4, 5]) # 데이터 뒤에 추가
data
```

* BFS 코드
```python
def bfs(graph, start_node):
    visited = list()
    need_visit = list()
    
    need_visit.append(start_node)
    
    while need_visit:  #need_visit 이 0이면 key값을 다 순회한 것
        node = need_visit.pop(0)
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])   # key가 a인 경우 a의 child nodes인 b,c가 추가
    
    return visited
```

* 시간복잡도
```python
def bfs(graph, start_node):
    visited = list()
    need_visit = list()
    
    need_visit.append(start_node)
    count = 0
    while need_visit:
        count += 1
        node = need_visit.pop(0)
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])
    print (count)
    return visited
```
- 위 코드에서 while need_visit 은 V + E 번 만큼 수행함  
	- 간선의 수 :9 노드의 수: 10  
	- 시간복잡도 : $O(19)$  