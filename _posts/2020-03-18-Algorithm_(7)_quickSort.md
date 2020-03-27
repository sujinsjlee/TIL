---
title: "Algorithm - (7) 퀵 소트"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
link: https://mg729.github.io/algorithm/2020/03/18/Algorithm_(7)_quicksort/
---

## 퀵 정렬 (Quick sort)  
> **퀵!소트**인만큼 시간복잡도가 낮다    
> 1. 데이터중에서 **기준점(pivot 이라고 부름)**을 정해서, 기준점보다 작은 데이터는 왼쪽(left), 큰 데이터는 오른쪽(right) 으로 모으는 함수를 작성함  
> 2. 각 왼쪽(left), 오른쪽(right)은 **재귀용법**을 사용해서 다시 동일 함수를 호출하여 위 작업을 반복함  
> 3. 함수는 왼쪽(left) + 기준점(pivot) + 오른쪽(right) 을 리턴함  


[![quick_sort](https://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Quicksort-diagram.svg/800px-Quicksort-diagram.svg.png)](https://en.wikipedia.org/wiki/Quicksort)



* 핵심 - **피봇** 이있고 피봇기준으로 왼쪽오른쪽으로 데이터를 나눈다    
* 그리고 **재귀적으로** 위 작업을 수행한다.  
* 피봇은 rule에 따라서 설정하는데 보통 맨 앞데이터, 맨 뒤 데이터를 피봇으로 설정  


## 시간 복잡도

병합정렬과 유사, 시간복잡도는 O(n log n)  
  - 단, 최악의 경우   
    - 맨 처음 pivot이 가장 크거나, 가장 작으면  
    - 모든 데이터를 비교하는 상황이 나옴  
    - $O(n^2)$  

## Pseudocode for Python

* quicksort 함수 만들기  
  - 만약 리스트 갯수가 한개이면 해당 리스트 리턴  
  - 그렇지 않으면, 리스트 맨 앞의 데이터를 기준점(pivot)으로 놓기  
  - left, right 리스트 변수를 만들고,  
  - 맨 앞의 데이터를 뺀 나머지 데이터를 기준점과 비교(pivot)  
    - 기준점보다 작으면 left.append(해당 데이터)  
    - 기준점보다 크면 right.append(해당 데이터)  
  - return quicksort(left) + pivot + quicksort(right) 로 재귀 호출  
> 리스트로 만들어서 리턴하기: return quick_sort(left) + [pivot] + quick_sort(right)  
{: .notice--primary}

### Python code implementation

* python solution (1)

```python
def qsort(data):
    if len(data) <= 1:
        return data
    
    left, right = list(), list()
    pivot = data[0]
    
    for index in range(1, len(data)):
        if pivot > data[index]:
            left.append(data[index])
        else:
            right.append(data[index])
    
    return qsort(left) + [pivot] + qsort(right)
```

* python solution (2)

```python
def qsort(data):
    if len(data) <= 1:
        return data
    
    pivot = data[0]

    left = [ item for item in data[1:] if pivot > item ]
    right = [ item for item in data[1:] if pivot <= item ]
    
    return qsort(left) + [pivot] + qsort(right)
```

```python
import random

data_list = random.sample(range(100), 10)

qsort(data_list)
```
## Analysis for C++ code 
1. 마지막 데이터를 피벗으로 선택
2. 왼쪽(i)에서 오른쪽으로 가면서 피벗보다 작은 수 찾음
3. 각 인덱스 i, j에 대한 요소를 교환
4. 2,3번 과정 반복
5. 더이상 2,3번 진행이 불가능하면, 현재 피벗과 교환
6. 이제 교환된 피벗 기준으로 왼쪽엔 피벗보다 작은 값, 오른쪽엔 큰 값들만 존재함
{: .notice--warning}

## C++ code implementation  
```cpp
#include<iostream>
using namespace std;

void swap(int* a, int* b);

int quickSplit(int* data, int low, int high)  
{  
    int pivot = data[high]; //last element as pivot
    int i = low; // Index of smaller element
    
    for (int j = low; j < high; j++)
    {
        // If current element is smaller than the pivot
        if (data[j] < pivot)
        {
            i++; // increment index of smaller element
            swap(&data[i-1], &data[j]);
        }
    }
    swap(&data[i], &data[high]);
    return i;
}

void quickSort(int* data, int start, int end)
{
	if(start >= end)
		return;
	
	//index means the pivot data's index of the result for quickSplit 
	int index = quickSplit(data, start, end); 
	
	quickSort(data, start, index-1);
	quickSort(data, index+1, end);
	
}
int main()
{
	int list_q[] = {5,3,1,8,7,4,9,2};
	
	int len = sizeof(list_q) / sizeof(list_q[0]);
	cout  << len << endl;
		
	quickSort(list_q, 0, len-1);
	
	for(int i = 0; i < len; ++i)
		cout << list_q[i] << " ";
		
	return 0;
	
}

void swap(int* a, int* b)  
{  
    int temp = *a;  
    *a = *b;  
    *b = temp;  
}
```

[quick_sort_geeksforgeeks](https://www.geeksforgeeks.org/quick-sort/)
