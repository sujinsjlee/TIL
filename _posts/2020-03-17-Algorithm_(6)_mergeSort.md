---
title: "Algorithm - (6) 병합 정렬"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
---

## 병합 정렬 (merge sort)
> **병합 정렬(합병 정렬)**: 합병정렬이라고도 부르며, 분할 정복방법을 통해 구현  
> 큰 문제를 작은 문제로단위로 분리, 정렬, 합병(취합)하는 알고리즘  
> 요소를 쪼갠 후 다시 합병시키면서 정렬해나가는 방식    


<center>
	<a href="https://en.wikipedia.org/wiki/Merge_sort">
		<img src="https://upload.wikimedia.org/wikipedia/commons/c/cc/Merge-sort-example-300px.gif"/>
	</a>
</center>


*동적계획법은 아닙니다.*  
**재귀용법**을 활용한 정렬 알고리즘  
1. 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 분리  
2. 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬  
3. 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병  

## 퀵소트와의 차이점
> **퀵정렬**: 우선 *pivot*을 통해 영역을 분할 후 정렬  
> **합병정렬**: 영역을 쪼갤 수 있을 만큼 분할 후 정렬  


## 알고리즘 분석  
* 데이터가 네 개 일때 
  - data_list = **[1, 9, 3, 2]**  
    - 먼저 **[1, 9], [3, 2]** 로 나누고  
    - 다시 앞 부분은 **[1], [9]** 로 나누고  
    - 다시 정렬해서 합친다. **[1, 9]**  
    - 다음 **[3, 2]** 는 **[3], [2]** 로 나누고  
    - 다시 정렬해서 합친다 **[2, 3]**  
    - 이제 **[1, 9]** 와 **[2, 3]**을 합친다.  
      - 1 < 2 이니 **[1]**  
      - 9 > 2 이니 **[1, 2]**  
      - 9 > 3 이니 **[1, 2, 3]**  
      - 9 밖에 없으니, **[1, 2, 3, 9]**  
{: .notice--info}


## Pseudocode
* **mergesort함수 만들기**
  - 만약 리스트 갯수가 한개이면 해당 값 리턴
  - 그렇지 않으면, 리스트를 앞뒤, 두 개로 나누기
  - left = mergesort(앞)
  - right = mergesort(뒤)
  - merge(left, right)

* **merge 함수 만들기**
  - 리스트 변수 하나 만들기 (sorted)
  - left_index, right_index = 0
  - while left_index < len(left) or right_index < len(right):
    - 만약 left_index 나 right_index 가 이미 left 또는 right 리스트를 다 순회했다면, 그 반대쪽 데이터를 그대로 넣고, 해당 인덱스 1 증가
    - if left[left_index] < right[right_index]:
      - sorted.append(left[left_index])
      - left_index += 1
    - else:
      - sorted.append(right[right_index])
      - right_index += 1
	  

## Time Complexity
- 몇 단계 깊이까지 만들어지는지를 depth 라고 하고 i라고 함   
- 맨 위 단계는 0  
  - n/$2^2$ 는 2단계 깊이  
  - 각 단계에 있는 하나의 노드 안의 리스트 길이는 n/$2^2$  
  - 각 단계에는 $2^i$ 개의 노드가 있음  
- 따라서, 각 단계는 항상 $2^i * \frac { n }{ 2^i } = O(n)$  
- 단계는 항상 $log_2 n$ 개 만큼 만들어짐, 시간 복잡도는 결국 $O(log n)$, 2는 역시 상수이므로 삭제  
- 따라서, 단계별 시간 복잡도 $O(n) * O(log n) = O(n log n)$   

## C++ code implementation  
```cpp
#include<iostream>
#include<cstdio>

using namespace std;

void merge(int * data, int * left, int * right, int medium, int size)
{
	int left_point = 0;
	int right_point = 0;
	int data_point = 0;
	// when left and right both have datas
	while(left_point < medium && right_point < size-medium)
	{
		if(left[left_point] > right[right_point])
		{
			data[data_point] = right[right_point];
			right_point++;
			data_point++;
		}
		else
		{
			data[data_point] = left[left_point];
			left_point++;
			data_point++;
		}
	}
	// only left has data
	while(left_point < medium)
	{
		data[data_point] = left[left_point];
		left_point++;
		data_point++;
	}
	// only right has data
	while(right_point < size-medium)
	{
		data[data_point] = right[right_point];
		right_point++;
		data_point++;
	}
}

void mergeSort(int * data, int size)
{
	if(size == 1)
		return;
	
	int medium = size/2;
	int leftData[medium];
	int rightData[size - medium];
	
	for(int i = 0; i < medium; ++i)
	{
		leftData[i] = data[i];
	}
	
	for(int i = 0; i < size - medium; ++i)
	{
		rightData[i] = data[medium + i];
	}
	
	//Divide
	mergeSort(leftData, medium); 
	mergeSort(rightData, size - medium);
	//Merge
	merge(data, leftData, rightData, medium, size);
	
}
int main()
{
	int list_s[] = {1,9,3,2};
	
	int len = sizeof(list_s) / sizeof(list_s[0]);
	cout  << len << endl;
	
	for(int i = 0; i < len; ++i)
		cout << list_s[i]<< " ";
	cout << endl;
	
	mergeSort(list_s, len);
	
	for(int i = 0; i < len; ++i)
		cout << list_s[i] <<" ";
	cout <<endl;	
		
	return 0;
	
}
```
* [merge_sort_geeksforgeeks](https://www.geeksforgeeks.org/merge-sort/)  

### Python code implementation

```python
def merge(left, right):
    merged = list()
    left_point, right_point = 0, 0
    
    # case1 - left/right 둘다 있을때
    while len(left) > left_point and len(right) > right_point:
        if left[left_point] > right[right_point]:
            merged.append(right[right_point])
            right_point += 1
        else:
            merged.append(left[left_point])
            left_point += 1

    # case2 - left 데이터가 없을 때
    while len(left) > left_point:
        merged.append(left[left_point])
        left_point += 1
        
    # case3 - right 데이터가 없을 때
    while len(right) > right_point:
        merged.append(right[right_point])
        right_point += 1
    
    return merged


def mergesort(data):
    if len(data) <= 1:
        return data
    medium = int(len(data) / 2)
    left = mergesort(data[:medium])
    right = mergesort(data[medium:])
    return merge(left, right)
```

```python
import random

data_list = random.sample(range(100), 10)
mergesort(data_list)
```
