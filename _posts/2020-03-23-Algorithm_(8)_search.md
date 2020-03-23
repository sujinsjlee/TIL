---
title: "Algorithm - (8) 순차탐색과 이진탐색"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
---

## 순차탐색 (Sequential Search)
> **탐색**은 여러 데이터 중에서 원하는 데이터를 찾아내는 것을 의미  
> **순차 탐색**: 데이터가 담겨있는 리스트를 앞에서부터 하나씩 비교해서 원하는 데이터를 찾는 방법  


* 시간 복잡도  
	* 최악의 경우 리스트 길이가 n일 때, n번 비교해야 함  
	* $O(n)$  

* C++ example   

```cpp
#include<iostream>
#include<cstdio>

using namespace std;

bool sequentialSearch(int* data, int size, int key)
{
	for(int i = 0; i < size; ++i)
	{
		if(data[i] == key)
		{
			return true;
		}
	}
	return false;
}

int main()
{
	int list_s[] = {5,4,3,2,1};
	
	int len = sizeof(list_s) / sizeof(list_s[0]);
	
	if(sequentialSearch(list_s, len, 3))
		cout << "search success" << endl;
	else
		cout << "search fail" << endl;
}
```

* Python example  

```python
from random import *

rand_data_list = list()
for num in range(10):
    rand_data_list.append(randint(1, 100))
```

```python
def sequencial(data_list, search_data):
    for index in range(len(data_list)):
        if data_list[index] == search_data:
            return index
    return -1
```

## 이진탐색 (Binary Search)
> **이진 탐색**: 탐색할 자료를 **둘**로 나누어 해당 데이터가 있을만한 곳을 탐색하는 방법  
> 분할 정복 알고리즘  


<center>
	<a href="https://en.wikipedia.org/wiki/Binary_search_algorithm">
		<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Binary_Search_Depiction.svg/1920px-Binary_Search_Depiction.svg.png"/>
	</a>
</center>



* 이진 탐색  
	* **Divide** : 데이터 리스트를 두개의 서브리스트로 나눈다  
	* **Conqure**  
		* 검색할 숫자 > 중간값 :  뒷 부분의 서브 리스트에서 검색할 숫자 탐색  
		* 검색할 숫자 < 중간값 :	앞 부분의 서브 리스트에서 검색할 숫자 탐색  
		
		
## Analysis  
* 이진 탐색은 데이터가 **정렬되있는 상태**에서 진행  
* 데이터가 [2, 3, 8, 12, 20] 일 때,  
- binary_search(data_list, find_data) 함수를 만들고  
	- find_data는 찾는 숫자  
	- data_list는 데이터 리스트  
	- data_list의 중간값을 find_data와 비교해서  
		- find_data < data_list의 중간값 이라면  
			- 맨 앞부터 data_list의 중간까지 에서 다시 find_data 찾기  
		- data_list의 중간값 < find_data 이라면  
		- data_list의 중간부터 맨 끝까지에서 다시 find_data 찾기  
		- 그렇지 않다면, data_list의 중간값은 find_data 인 경우로, return data_list 중간위치  
{: .notice--primary}

## 알고리즘 시간 복잡
* n개의 리스트를 매번 2로 나누어 1이 될 때까지 비교연산을 k회 진행
	- n X $\frac { 1 }{ 2 }$ X $\frac { 1 }{ 2 }$ X $\frac { 1 }{ 2 }$ ... = 1
	- n X $\frac { 1 }{ 2 }^k$ = 1
	- n = $2^k$ = $log_2 n$ = $log_2 2^k$
	- $log_2 n$ = k  
	- 빅 오 표기법으로는 k + 1 이 결국 최종 시간 복잡도임 (1이 되었을 때도, 비교연산을 한번 수행)  
		- 결국 $O(log_2 n + 1)$ 이고, 2와 1, 상수는 삭제 되므로, $O(log n)$  
{: .notice--info}

## C++ 

```cpp

```


## Python

```python
def binary_search(data, search):
    print (data)
    if len(data) == 1 and search == data[0]:
        return True
    if len(data) == 1 and search != data[0]:
        return False
    if len(data) == 0:
        return False
    
    medium = len(data) // 2
    if search == data[medium]:
        return True
    else:
        if search > data[medium]:
            return binary_search(data[medium+1:], search)
        else:
            return binary_search(data[:medium], search)
```

```python
import random
data_list = random.sample(range(100), 10)
data_list
data_list.sort() 
data_list

binary_search(data_list, 66)
```

