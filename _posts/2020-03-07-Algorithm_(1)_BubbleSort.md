---
title: "Algorithm - (1) 버블 정렬"
categories:
  - Algorithm
tags:
  - Algorithm
---
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    TeX: {
      equationNumbers: {
        autoNumber: "AMS"
      }
    },
    tex2jax: {
    inlineMath: [ ['$', '$'] ],
    displayMath: [ ['$$', '$$'] ],
    processEscapes: true,
  }
});
MathJax.Hub.Register.MessageHook("Math Processing Error",function (message) {
	  alert("Math Processing Error: "+message[1]);
	});
MathJax.Hub.Register.MessageHook("TeX Jax - parse error",function (message) {
	  alert("Math Processing Error: "+message[1]);
	});
</script>
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

## 버블 정렬
> **버블 정렬**: 두 인접한 데이터를 비교해서, 앞에 있는 데이터가 뒤에있는 데이터보다 크면, 자리를 바꾸는 정렬 알고리즘  

<center>
	<a href="https://en.wikipedia.org/wiki/Bubble_sort">
		<img src="https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif"/>
	</a>
</center>
<!--
![](https://upload.wikimedia.org/wikipedia/commons/c/c8/Bubble-sort-example-300px.gif)](https://en.wikipedia.org/wiki/Bubble_sort)
-->   
<!--The link - reference : (https://en.wikipedia.org/wiki/Bubble_sort)-->

## 코드 디자인  
* __조건체크__ : 두 개의 데이터의 크기비교  
* __turn__ : 전체 데이터 리스트에 대한 swapping비교하는 turn (전체 데이터를 총 조건체크하는 한 번의 로테이션)  


1. 데이터가 **두 개**일 때 버블 정렬  
(3 2)  
(2 __3__)  
`조건체크 : 1`  
`turn : 1`  
2. 데이터가 **세 개**일 때 버블 정렬   
(5 4 3)  
(4 3 __5__)  
(3 __4__ __5__)  
`조건체크 : 2`  
`turn : 2`  
3. 데이터가 **네 개**일 때 버블 정렬  
(5 4 3 2)  
(4 3 2 __5__)  
(3 2 __4__ __5__)  
(2 __3__ __4__ __5__)  
`조건체크 : 3`  
`turn : 3`  
{: .notice--info}

## 버블 정렬 알고리즘 (Pseudocode)  
```cpp
for(int n = 0; n < 데이터 길이 -1; n++)
{
   bool swaps = false;
	for(int index = 0; index < 데이터 길이 - n -1 ; index++)
   {
	   if(앞 데이터 > 뒤 데이터)
	      swap two datas;
      	swaps = true;		
   }
   if(!swaps)
      break;
}
```	
{: .notice--success}
* `length of the entire data - n -1`  
   * __-n__ : -n을 하는 이유는 한 번의 턴을 거칠 때마다 뒤에 있는 데이터는 정렬이 되기때문에 정렬되지 않은 데이터에대해서만 조건체크를 하기 위함  

1. for num in range(len(data_list)) 반복
2. swap = false (교환이 되었는지를 확인하는 변수를 두자)
3. 반복문 안에서, for index in range(len(data_list) - num - 1) n - 1번 반복해야 하므로
4. 반복문안의 반복문 안에서, if data_list[index] > data_list[index + 1] 이면
5. __swapping__ : data_list[index], data_list[index + 1] = data_list[index + 1], data_list[index]
6. swap = true
7. 반복문 안에서, if swap == false 이면, break 끝

## 알고리즘 시간복잡도
> 반복문이 두 개 : **O(n^2)**  

완전 정렬이 되어있는 상태라면 최선의 시간복잡도는 O(n)  

## C++ 코드 구현 
```cpp
#include<iostream>
using namespace std;

void bubbleSort(int * data, int size)
{
	for(int i = 0; i < size-1 ; ++i)
	{
		bool swaps = false;
		for(int index = 0; index < size - i - 1; ++index)
		{
			if(data[index] > data[index+1])
			{
				int temp = data[index];
				data[index] = data[index+1];
				data[index+1] = temp;
			}
			swaps = true;
		}
		if(!swaps)
			break;
	}
}
int main()
{
	int list_b[] = {5,4,3,2,1};
	
	int len = sizeof(list_b) / sizeof(list_b[0]);
	cout  << len << endl;
	
	for(int i = 0; i < len; ++i)
		cout << list_b[i] << endl;
		
	bubbleSort(list_b, len);
	
	for(int i = 0; i < len; ++i)
		cout << list_b[i] << endl;
		
		
	return 0;
	
}
```

[Bubble sort code](https://www.tutorialspoint.com/cplusplus-program-to-implement-bubble-sort)
```cpp
#include<iostream>
using namespace std;
void swapping(int &a, int &b) {      //swap the content of a and b
   int temp;
   temp = a;
   a = b;
   b = temp;
}
void display(int *array, int size) {
   for(int i = 0; i<size; i++)
      cout << array[i] << " ";
   cout << endl;
}
void bubbleSort(int *array, int size) {
   for(int i = 0; i<size; i++) {
      int swaps = 0;         //flag to detect any swap is there or not
      for(int j = 0; j<size-i-1; j++) {
         if(array[j] > array[j+1]) {       //when the current item is bigger than next
            swapping(array[j], array[j+1]);
            swaps = 1;    //set swap flag
         }
      }
      if(!swaps)
         break;       // No swap in this pass, so array is sorted
   }
}
int main() {
   int n;
   cout << "Enter the number of elements: ";
   cin >> n;
   int arr[n];     //create an array with given number of elements
   cout << "Enter elements:" << endl;
   for(int i = 0; i<n; i++) {
      cin >> arr[i];
   }
   cout << "Array before Sorting: ";
   display(arr, n);
   bubbleSort(arr, n);
   cout << "Array after Sorting: ";
   display(arr, n);
}
```


