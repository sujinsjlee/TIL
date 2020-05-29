---
title: "C++ - 2차원 벡터 선언 및 초기화"
published: false
categories:
  - C++
tags:
  - C++
<!--link: --> 
---

<!-- BOJ 12865.cpp -->


C++에서 2차원 vector를 동적으로 할당하는 방법은 여러가지가 있다.

내가 가장 편하게 사용하는 것외에도 정리해놓자!

 

 

방법0.  내가 가장 편하게 생각하는 방법

n*n 이중 배열 만들기 

: 행과 열의 크기가 같은 이중배열 만드는 방법

#include<vector>
using namespace std;
vector<vector<int>> arr; 
arr.assign(n, vector<int>(n, 0)); 
코드 설명

- arr 이중 벡터를 선언한다. 

- arr[n][n] 을 할당하고, 0으로 초기화한다.

 

 

방법1.

 

n*n 이중 배열 만들기

#include<vector>
vector<vector<int>> arr;
for(int i=0; i<n; i++){
  vector<int>element(n);
  arr.push_back(element);
}
코드설명

- arr 이중 벡터를 선언한다.

- arr[n][n]을 할당한다.

 

위의 코드 예제에서는 n*n으로 생성하였지만,

각 행에 할당된 열의 개수가 동일하지 않게 생성이 가능하다. 아래 표 참고.


 

 

방법2.

 

행과 열 사이즈 다른 배열 만들기

#include<vector>
vector< vector<int>> 
arr(6, vector<int>(5,0));
 코드설명

- int arr[6][5] 배열을 선언하고, 0으로 초기화한다.



출처: https://flower0.tistory.com/42 [flower0]