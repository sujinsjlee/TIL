---
title: "Algorithm - (2) 선택 정렬"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
link: https://sujinsjlee.github.io/algorithm/2020/03/08/Algorithm_(2)_SelectionSort/
---

## 선택 정렬

> 선택 정렬 : 최소값을 **선택**한다! 해서 선택정렬  


* 선택 정렬 알고리즘  
	* 주어진 데이터에서 최소 값을 찾음  
	* 해당 최소값을 데이터 맨 앞에 위치한 값과 교체  
	* 맨 앞의 위치를 뺀 나머지 데이터를 동일한 방법으로 반복  

<center>
	<a href="https://en.wikipedia.org/wiki/Selection_sort">
		<img src="https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif"/>
	</a>
</center>


## 코드 디자인  
> **데이터 앞쪽 부터 정렬**  
> 매번 반복문을 실행할때마다 이전 반복문에서의 첫번째 인덱스값을 제외하고 정렬함    
> __turn__ : 전체 데이터 리스트에 대한 swapping비교하는 turn (전체 데이터를 총 조건체크하는 한 번의 로테이션)  


1. **데이터가 *두 개*일 때 선택 정렬**  
(3 2)  
(**2** 3)  

	| 비교데이터 인덱스  | 비교 시작 데이터  | 비교 끝 데이터  |
	| :---: | :---: | :---: |
	| 0   | 1           | 1   |
2. **데이터가 *세 개*일 때 선택 정렬**   
(3 4 2)  
(**2** 4 3)  
(**2** **3** 4)  

	| 비교데이터 인덱스  | 비교 시작 데이터  | 비교 끝 데이터  |
	| :---: | :---: | :---: |
	| 0   | 1           | 2   |
	| 1   | 2           | 2  |  
3. **데이터가 *네 개*일 때 선택 정렬**  
(4 5 3 2)  
(**2** 5 3 4)  
(**2 3** 5 4)  
(**2 3 4** 5)   

	| 비교데이터 인덱스  | 비교 시작 데이터  | 비교 끝 데이터  |
	| :---: | :---: | :---: |
	| 0   | 1           | 3   |
	| 1   | 2           | 3   |
	| 2   | 3           | 3   |
{: .notice--info}

## 선택 정렬 알고리즘 (Pseudocode)  
```cpp
for(int standard = 0; standard < 데이터길이 - 1; ++standard) //turn
{
	int lowest = standard;
	for(int index = standard+1; index < 데이터길이 ; ++index)
		if(data[lowest] > data[index])
			lowest = index;
	
	swapping data[lowest] and data[standard]
}
```	

1. for standard in range(len(data_list) - 1) 로 반복
2. lowest = standard 로 놓고,
3. for index in range(standard, len(data_list)) standard 이후부터 반복
	* 내부 반복문 안에서 data_list[lowest] > data_list[index] 이면,
		* lowest = index
4. swapping two data  
	* data_list[index], data_list[lowest] = data_list[lowest], data_list[num]  
{: .notice--success}



## 알고리즘 시간복잡도
> 반복문이 두 개 : **$O(n^2)$**  

## C++ 코드 구현 
```cpp
#include<iostream>
using namespace std;

void selectionSort(int * data, int size)
{
	for(int standard = 0; standard < size-1 ; ++standard)  //turn 
	{
		int lowest = standard;
		for(int index = standard+1; index < size; ++index)
		{
			if(data[lowest] > data[index])
				lowest = index;
		}
		int temp = data[lowest];
		data[lowest] = data[standard];
		data[standard] = temp;
	}
}
int main()
{
	int list_s[] = {4,5,3,2,1};
	
	int len = sizeof(list_s) / sizeof(list_s[0]);
	cout  << len << endl;
	
	for(int i = 0; i < len; ++i)
		cout << list_s[i] << endl;
		
	selectionSort(list_s, len);
	
	for(int i = 0; i < len; ++i)
		cout << list_s[i] << endl;
		
		
	return 0;
	
}
```

## Python 코드 구현
```python
def selection_sort(data):
    for standard in range(len(data) - 1):
        lowest = standard
        for index in range(standard + 1, len(data)):
            if data[lowest] > data[index]:
                lowest = index
        data[lowest], data[standard] = data[standard], data[lowest]
    return data
```