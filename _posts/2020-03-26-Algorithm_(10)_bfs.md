---
title: "Algorithm - (10) BFS"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
link: https://mg729.github.io/algorithm/2020/03/26/Algorithm_(9)_bfs/
---

## BFS (Breadth-First Search)   
* 대표적인 그래프 **탐색** 알고리즘  
- 너비 우선 탐색 (Breadth First Search): 정점들과 같은 레벨에 있는 노드들 (형제 노드들)을 먼저 탐색하는 방식  
- 깊이 우선 탐색 (Depth First Search): 정점의 자식들을 먼저 탐색하는 방식  

<center>
	<a href="https://en.wikipedia.org/wiki/Breadth-first_search">
		<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/Breadth-first-tree.svg/450px-Breadth-first-tree.svg.png"/>
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
#include<iostream>
#include<cstdio>
#include<vector> //to store data
#include<queue>

using namespace std;

int number = 7;
int visited[7]; 
vector<int> need_visit[8];
 
void bfs(int start)
{
	queue<int> q;
	q.push(start);
	
	visited[start] = true;
	while(!q.empty())
	{
		int x = q.front();
		q.pop();
		printf("%d ", x);
		
		for(int i = 0; i < need_visit[x].size(); ++i)
		{
			int y = need_visit[x][i];
			if(!visited[y])
			{
				q.push(y);
				visited[y] = true;
			}
		}
	}
}
int main()
{
	need_visit[1].push_back(2);
	need_visit[2].push_back(1);
	
	need_visit[1].push_back(3);
	need_visit[3].push_back(1);
	
	need_visit[1].push_back(4);
	need_visit[4].push_back(1);
	
	need_visit[2].push_back(5);
	need_visit[5].push_back(2);

	need_visit[2].push_back(6);
	need_visit[6].push_back(2);
	
	need_visit[4].push_back(7);
	need_visit[7].push_back(4);
	
	need_visit[4].push_back(8);
	need_visit[8].push_back(4);
	
	need_visit[5].push_back(9);
	need_visit[9].push_back(5);

	need_visit[5].push_back(10);
	need_visit[10].push_back(5);	
		
	need_visit[7].push_back(11);
	need_visit[11].push_back(7);
	
	need_visit[7].push_back(12);
	need_visit[12].push_back(7);
	
	bfs(1);
	
	return 0;
}
```
`int visited[7];`   
	* visited 배열 원소를 모두 0 (false)로 초기화   
`vector<int> need_visit[8];`   
	* 그래프 인덱스가 1부터 시작하도록 설정    

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
	