---
title: "Algorithm - (15) Dijkstra"
categories:
  - Algorithm
tags:
  - Algorithm
---

- 다익스트라 알고리즘은 다이나믹 프로그래밍을 활용한 대표적인 최단 경로 탐색알고리즘
    - **다이나믹프로그래밍** : 큰 문제를 한 번에 해결하기 힘들 때 작은 여러 개의 문제로 나누어서 푸는 기법
- 흔히 인공위성 GPS 소프트웨어등에서 가장 많이 사용
- 하나의 최단거리를 구할 때 그 이전까지 구했던 최단거리 정보를 그대로 사용

- **다익스트라**
    - 출발노드를 설정
    - 출발노드를 기준으로 각 노드의 최소비용을 저장
    - 방문하지 않은 노드 중에서 가장 적은 비용의 노드를 선택
    - 해당노드를 거쳐서 특정한 노드로 가는 경우를 고려하여(이 때 이전까지 구했던 최단 거리정보를 활용하여) 최소 비용을 갱신

- EXAMPLE

```c++

#include<bits/stdc++.h>

using namespace std;

int n, m, a, b, e;

struct Graph{
	int vertex;
	int edge;
	Graph(int ve, int ed) {
		vertex = ve;
		edge = ed;
	}
	bool operator < (const Graph& cmpGraph) const {
		return edge > cmpGraph.edge;
	}
};

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	
	freopen("input.txt", "rt", stdin);
	
	cin >> n >> m;
	vector<Graph> v[22];
	for(int i = 0; i < m; i++) {
		cin >> a >> b >> e;
		v[a].push_back({b,e});
	}

	vector<int> cost(22, 2147000000); // need to initialize all the data as 2147000000 by vector
	
	priority_queue<Graph> pq;
	pq.push({1, 0});
	cost[1] = 0;
	
	// below while code is Dijkstra algorithm
	while(!pq.empty()){
		int curNode = pq.top().vertex;
		int curCost = pq.top().edge;
		pq.pop();
		if(cost[curNode] < curCost) continue;
		for(int i = 0; i < v[curNode].size(); i++) {
			int nextNode = v[curNode][i].vertex;
			int nextCost = curCost + v[curNode][i].edge;
			if(nextCost < cost[nextNode]) {
				cost[nextNode] = nextCost;
				pq.push({nextNode, nextCost});
			}
		}
	}
	
	for(int i = 2 ; i <= n; i++) {
		if(cost[i] == 2147000000) cout <<"impossible";
		else cout << i << " : " << cost[i] << "\n";
	}

 	return 0;
}

```