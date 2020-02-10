---
title: "Data Structure - (2) 배열"
categories:
  - Data Structure
tags:
  - Data Structure
link: https://mg729.github.io//datastructure/2020/01/11/DataStructure_(2)_Array/
---

##  Array  
>**같은 데이터 타입의 데이터를 나열하고, 각 데이터를 인덱스에 대응하도록 구성한 데이터 구조**  

같은 종류의 데이터를 효율적으로 순차적으로 처리  
인덱스를 활용하여 나열된 데이터의 일부분에 바로 접근 가능  
_Array stores a fixed-size sequential collection of elements of the same type._ 

## 배열의 장점  
* 인덱스 번호를 활용한 빠른 접근가능  

## 배열의 단점  
* 데이터가 가변적인 경우 데이터의 추가, 삭제 쉽지 않음  
고정된 크기의 공간이 선언되어있기 때문에 배열의 최대 길이를 모른다면 새로운 데이터 추가가 어려움  
데이터를 삭제하고나서 기존 뒤의 데이터를 앞으로 당겨여하는 문제가 있음   
* 배열타입의 데이터 선언할 때 미리 최대 길이의 size를 지정해야함  

## 예제 (C++)
아래의 dataset 내부에서 'M'이 몇 번 나왔는지에 대한 빈도 수 출력  

{% highlight c++ %}
#include<stdio.h>

int main()
{
	char dataset[][70] = {"Jennifer Anniston, Ms. Jen",
		"Courtney Cox, Ms. Cox",
		"Lisa Kudrow, Ms. Kudrow",
		"Matthew Perry, Mr. Perry (Metthew)",
		"David Schwimmer, Mr. Schwimmer",
		"Matt LeBlanc, Mr. LeBlanc (Matt)"};
    int m = 0;
    
  	for(char* data : dataset)
    {
    	for(int i = 0; data[i] != '\0' ; i++)
    	{
			if( data[i] =='M')
			{
				m++;   		
			}
		}
	} 
	printf("%d\n", m); //10

	return 0;
}
{% endhighlight %}


* 2차원 배열과 포인터 배열  
[Two dimension array and Pointer array](http://www.parkjonghyuk.net/lecture/programming1/lecturenote/chap06-6.pdf).