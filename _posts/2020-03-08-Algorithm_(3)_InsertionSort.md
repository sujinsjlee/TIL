---
title: "Algorithm - (3) 삽입 정렬"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
link: https://sujinsjlee.github.io/algorithm/2020/03/08/Algorithm_(3)_InsertionSort/
---

## 삽입 정렬  
> **맨앞**에서부터 정렬이 되는 알고리즘  
> 데이터의 모든 요소를 **앞에서부터** 차례대로 이미 정렬된 부분과 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성하는 알고리즘  

* 삽입 정렬은 **두 번째 인덱스**부터 시작  
* 해당 인덱스(**key 값**) 앞에 있는 데이터(**A**)부터 비교
  * key 값이 더 작으면, A값을 뒤 인덱스로 복사  
* 이를 key 값이 더 큰 데이터를 만날때까지 반복  
  * 큰 데이터를 만난 위치 바로 뒤에 key 값을 이동  

<center>
	<a href="https://en.wikipedia.org/wiki/Insertion_sort">
		<img src="https://upload.wikimedia.org/wikipedia/commons/9/9c/Insertion-sort-example.gif"/>
	</a>
</center>

## Code Design   
> `index`  
> value  



* 데이터가 네 개 일때
  ### 1. (5 3 2 4)  
    `1 0`  
    3 5  
    (**3 5** 2 4)  

    | 기준 데이터 인덱스  | 비교 데이터 인덱스 |
    | :---: | :---: |
    | 1     | 0     |

  ### 2. (<u>3 5</u> 2 4)  
    `2 1`   
    2 5  
    (3 **2 5** 4)  
    `1 0`  
    2 3  
    (**2 3** 5 4)  

    | 기준 데이터 인덱스  | 비교 데이터 인덱스 |
    | :---: | :---: |
    | 2     | 1     |

  ### 3. (<u>2 3 5</u> 4)  
    `3 2`   
    4 5  
    (2 3 **4 5**)  
    `2 1`   
    4 3  
    ~~`1 0`~~    

    | 기준 데이터 인덱스  | 비교 데이터 인덱스 |
    | :---: | :---: |
    | 3     | 2     |

  ### 4. (<u>2 3 4 5</u>)  
{: .notice--info}

## 알고리즘 (Pseudocode)
```cpp
for(int i = 0; i < 데이터 길이 -1 ; ++i)
  for(int base = i+1; base != 0 ; ++i)
  {
      if(data[base] < data[base-1])
        swapping two datas
      else
        break;
  }
```

## 알고리즘 시간복잡도
* 반복문이 두 개 **O($n^2$)**  


## C++코드 구현
```cpp
#include<iostream>
using namespace std;

void insertionSort(int * data, int size)
{
	for(int i = 0; i < size-1 ; ++i )
	{
		for(int base = i+1 ; base != 0 ; --base)
		{
			if(data[base] < data[base-1])
			{
				int temp = data[base];
				data[base] = data[base-1];
				data[base-1] = temp;
			}
			else
				break;
		}
	}	
}
int main()
{
	int data_i[] = {4,5,3,2,1};

	int len = sizeof(data_i) / sizeof(data_i[0]);
	cout  << len << endl;

	for(int i = 0; i < len; ++i)
		cout << data_i[i] << endl;

	insertionSort(data_i, len);
	
	for(int i = 0; i < len; ++i)
		cout << data_i[i] << endl;
		
	return 0;
	
}
```

## Python 코드 구현
```python
def insertion_sort(data):
    for index in range(len(data) - 1):
        for index2 in range(index + 1, 0, -1): 
            if data[index2] < data[index2 - 1]:
                data[index2], data[index2 - 1] = data[index2 - 1], data[index2]
            else:
                break
    return data
```
* for index2 in range(index + 1, 0, -1)
  * -1씩줄여가면서 index+1 부터 0 직전, 즉 1번까지 for루프반복 
  * 기준점 1까지가야 1 0 도 비교
