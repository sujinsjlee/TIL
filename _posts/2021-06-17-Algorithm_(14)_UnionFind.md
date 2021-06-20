---
title: "Algorithm - (14) UnionFind"
categories:
  - Algorithm
tags:
  - Algorithm
---

## UnionFind 
> **UnionFind**  : *A disjoint-set* data strsubsetsucture is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) . A union-find algorithm is an algorithm that performs two useful operations on such a data structure


- Union Find 알고리즘 : Disjoint Set을 표현할 때 사용하는 알고리즘
    - Disjoint Set 서로소 집합 
    - **tree**로 구현합니다.
    
- Example

```c++
#include<bits/stdc++.h>
using namespace std;

int unf[1002]; // tree
int node1, node2;

int Find(int v) { //Find Parent Node
	if(unf[v] == v) return v;
	else return unf[v] = Find(unf[v]); //경로 압축 - memoization  
}

void Union(int a, int b) {
	node1 = Find(a);
	node2 = Find(b);
	
	if(node1 != node2) unf[node1] = node2; //organize tree structure
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	
	int n, m, x, y;
	freopen("input.txt", "rt", stdin);
	cin >> n >> m;
	for(int i = 1; i <= n; i++) {
		unf[i] = i; // initialize tree
	}
	
	for(int i = 1; i <= m; i++) {
		cin >> x >> y;
		Union(x, y);
	}
	
	cin >> x >> y;
	node1 = Find(x);
	node2 = Find(y);
	if(node1 != node2) cout << "Not in the same set"<< "\n"; // if parentNode not same, not in same set
	else cout << "In the same set"<< "\n"; // same parent node, same set
	
	for(int i = 1; i <= 5; i++) cout << unf[i] << " ";
	
 	return 0;
}
```


