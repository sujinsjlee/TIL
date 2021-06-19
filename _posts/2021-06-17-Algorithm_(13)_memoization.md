---
title: "Algorithm - (13) memoization"
categories:
  - Algorithm
tags:
  - Algorithm
---

## memoization
-  **메모이제이션(memoization)** 은 컴퓨터 프로그램이 동일한 계산을 반복해야 할 때, 이전에 계산한 값을 메모리에 저장함으로써 동일한 계산의 중복 수행을 제거하여 프로그램 실행 속도를 빠르게 하는 기술이다.

- 대표 예제 
    - **이항계수**
    - **nCr = n-1Cr + n-1Cr-1**
    - **nCn == nC0** : **1**
        - *n개 중 n개 모두를 선택하는 경우의수*와 *n개 중 아무것도 고르지 않는 경우의 수* 모두 1가지씩있으므로 nCn과 nC0은 1의 값을 가짐
    - 이미 계산된 조합의 결과는 중복계산하지 않도록 코딩

- 이항계수

```c++
#include<bits/stdc++.h>
using namespace std;

int memoi[22][22];

int dfs(int n, int r) {
	if(memoi[n][r]) return memoi[n][r];
	if(n == r || r == 0) return 1;
	else return memoi[n][r] = dfs(n-1, r) + dfs(n-1, r-1); // dfs(n-1, r) + dfs(n-1, r-1) 怨꾩궛??寃곌낵瑜?memoi[n][r] ????낇븯怨? memoi[n][r] ??return 
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr);
	
	freopen("input.txt", "rt", stdin);
	
	int n, r;
	cin >> n >> r;
	
	// nCr = n-1Cr + n-1Cr-1
	cout << dfs(n, r);	

 	return 0;
}
```

