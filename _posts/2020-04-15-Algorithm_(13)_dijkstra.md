---
title: "Algorithm - (13) 최단경로 알고리즘"
published: false
categories:
  - Algorithm
tags:
  - Algorithm
<!--link: --> 
---
## 1. 최단 경로 문제
- 최단 경로 문제란 두 노드를 잇는 가장 짧은 경로를 찾는 문제  
- 가중치 그래프 (Weighted Graph) 에서 간선 (Edge)의 가중치 합이 최소가 되도록 하는 경로를 찾는 것이 목적  

### 최단 경로 문제 종류
1. 단일 출발 및 단일 도착 (single-source and single-destination shortest path problem) 최단 경로 문제  
	- 그래프 내의 특정 노드 u 에서 출발, 또다른 특정 노드 v 에 도착하는 가장 짧은 경로를 찾는 문제  
2. 단일 출발 (single-source shortest path problem) 최단 경로 문제  
	- 그래프 내의 특정 노드 u 와 그래프 내 다른 모든 노드 각각의 가장 짧은 경로를 찾는 문제  
	> 예를 들어 A, B, C, D 라는 노드를 가진 그래프에서 특정 노드를 A 라고 한다면,  
	> A 외 모든 노드인 B, C, D 각 노드와 A 간에 (즉, A - B, A - C, A - D) 각각 가장 짧은 경로를 찾는 문제를 의미함  

3. 전체 쌍(all-pair) 최단 경로: 그래프 내의 모든 노드 쌍 (u, v) 에 대한 최단 경로를 찾는 문제  

## 2. 최단 경로 알고리즘 - 다익스트라 알고리즘
- 다익스트라 알고리즘은 위의 최단 경로 문제 종류 중, 2번에 해당  
	- 하나의 정점에서 다른 모든 정점 간의 각각 **가장 짧은 거리**를 구하는 문제  