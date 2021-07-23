---
title: "C++ - 조합"
categories:
  - C++
tags:
  - C++
---

## 조합 

```c++
#include<bits/stdc++.h>

using namespace std;

int n, r;
int ch[20];

void dfs(int s, int L) {
	if(L == r) {
		for(int i = 0; i < L ; i++) {
			cout << ch[i] << " ";
		}
		cout << endl;
	}
	else {
		for(int i = s; i < n; i++) {
			ch[L] = i;
			dfs(i+1,  L+1);
		}
	}
}

int main(){
	ios::sync_with_stdio(false);
	cin.tie(nullptr);

	freopen("input.txt", "rt", stdin);
	cin >> n >> r;
	
	dfs(0,0);
	
	return 0;
}
```