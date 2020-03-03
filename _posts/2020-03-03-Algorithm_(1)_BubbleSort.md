---
layout: post
title:  - (1) 버블 정렬
description: (1) Understanding of Bubble Sort
modified: 2020-03-03
tags: [Algorithm]
categories: [Algorithm]
published: false
---

## 버블 정렬
> **버블 정렬**: 두 인접한 데이터를 비교해서, 앞에 있는 데이터가 뒤에있는 데이터보다 크면, 자리를 바꾸는 정렬 알고리즘  

![Bubble sort](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)  
[wiki-Bubble_sort](https://en.wikipedia.org/wiki/Bubble_sort)

## 코드 디자인  
* __조건체크__ : 두 개의 데이터의 크기비교  
* __turn__ : 전체 데이터 리스트에 대한 swaping비교하는 turn (전체 데이터를 총 조건체크하는 한 번의 로테이션)  


1. 데이터가 두 개일 때 버블 정렬  
(3 2)  
(2 __3__)  
{: .notice--info}
`조건체크 : 1`  
`turn : 1`  

2. 데이터가 세 개일 때 버블 정렬   
(5 4 3)  
(4 3 __5__)  
(3 __4__ __5__)  
{: .notice--info}
`조건체크 : 2`  
`turn : 2`  

3. 데이터가 네 개일 때 버블 정렬  
(5 4 3 2)  
(4 3 2 __5__)  
(3 2 __4__ __5__)
(2 __3__ __4__ __5__) 
{: .notice--info}
`조건체크 : 3`  
`turn : 3`  


## 버블 정렬 알고리즘 (Pseudocode)  
```cpp
for(int n = 0; n < 데이터 길이 -1; n++)
	for(int index = 0; index < 데이터 길이 - n -1 ; index++)
		if(앞 데이터 > 뒤 데이터)
			swap
```	
{: .notice--success}
`length of the entire data - n -1`: __-n__ : -n을 하는 이유는 한 번의 턴을 거칠 때마다 뒤에 있는 데이터는 정렬이 되기때문에 정렬되지 않은 데이터에대해서만 조건체크를 하기 위함  

1. for num in range(len(data_list)) 반복
2. swap = 0 (교환이 되었는지를 확인하는 변수를 두자)
3. 반복문 안에서, for index in range(len(data_list) - num - 1) n - 1번 반복해야 하므로
4. 반복문안의 반복문 안에서, if data_list[index] > data_list[index + 1] 이면
5. data_list[index], data_list[index + 1] = data_list[index + 1], data_list[index]
6. swap += 1
7. 반복문 안에서, if swap == 0 이면, break 끝

## 알고리즘 시간복잡도
> 반복문이 두 개 : **O(n^2)**  

완전 정렬이 되어있는 상태라면 최선의 시간복잡도는 O(n)  

## C++ 코드 구현 
```cpp

```