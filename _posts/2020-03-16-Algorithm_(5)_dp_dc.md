---
title: "Algorithm - (5) 동적계획법과 분할 정복"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
---

## 동적 계획법 (Dynamic Programming)과 분할 정복 (Divide and Conquer)

> 동적계획법 (**DP** 라고 많이 부름)  
> 입력 크기가 작은 부분 문제들을 해결한 후, 해당 부분 문제의 해를 활용해서, 보다 큰 크기의 부분 문제를 해결, 최종적으로 전체 문제를 해결하는 알고리즘  


- **상향식 접근법**으로, 가장 최하위 해답을 구한 후, 이를 저장하고, 해당 결과값을 이용해서 상위 문제를 풀어가는 방식   
- Memoization 기법을 사용함  
	- **메모이제이션**이 핵심!!  
	- Memoization : 프로그램 실행 시 이전에 계산한 값을 저장하여, 다시 계산하지 않도록 하여 전체 실행 속도를 빠르게 하는 기술  
	- 문제를 잘게 쪼갤 때, 부분 문제는 중복되어, 재활용됨  
- 예: 피보나치 수열  
{: .notice--primary}

> 분할 정복 (Divide and Conquer)  
>문제를 나눌 수 없을 때까지 나누어서 각각을 풀면서 다시 합병하여 문제의 답을 얻는 알고리즘  


- **하향식 접근법**으로, 상위의 해답을 구하기 위해, 아래로 내려가면서 하위의 해답을 구하는 방식  
- 일반적으로 **재귀함수**로 구현  
  - 문제를 잘게 쪼갤 때, 부분 문제는 서로 중복되지 않음  
- 예: 병합 정렬, 퀵 정렬 등  
{: .notice--primary}

	
## 공통점과 차이점 
- **공통점**  
  - 문제를 잘게 쪼개서, 가장 작은 단위로 분할  
- **차이점**  
  - 동적 계획법  
    - 부분 문제는 중복되어, 상위 문제 해결 시 재활용  
    - Memoization 기법 사용 (부분 문제의 해답을 저장해서 재활용하는 최적화 기법으로 사용)  
  - 분할 정복  
    - 부분 문제는 서로 중복되지 않음  
    - Memoization 기법 사용 안함  
{: .notice}


## 다이나믹 프로그래밍 이해  
> **피보나치 수열**  
> 피보나치 수는 첫째 항은 0 둘째 항이 1이며 그 뒤의 모든 항은 바로 앞 두 항의 합인 수열   
> *0,1,1,2,3,5,8,13,21,34,55,89,144,...*  


F_0=0  
F_1=1  
F_n=F_{n-1}+F_{n-2}\qquad(n\in\{2,3,4,\dots\})  

1. 분할 정복  
```cpp
#include<iostream>
#include<cstdio>

using namespace std;

int fibo(int n)
{
	if(n == 0)
		return 0;
	else if(n == 1)
		return 1;

	return fibo(n-1) + fibo(n-2);
}
int main()
{
	int n;
	cin >> n;
	
	cout << fibo(n) << endl;
	
	return 0;
}
```


2. 동적 계획법
* C++  

```cpp
#include<iostream>
#include<cstdio>

using namespace std;

int fibo(int n)
{
	int cache[n];
	
	cache[0] = 0;
	cache[1] = 1;
	
	for(int i = 2; i <= n; ++i)
	{
		cache[i] = cache[i-1] + cache[i-2];
	}
	
	return cache[n];
}
int main()
{
	int n;
	cin >> n;
	
	cout << fibo(n) << endl;
	
	return 0;
}
```

* Python  
```python
def fibo_dp(num):
    cache = [ 0 for index in range(num + 1)]
    cache[0] = 0
    cache[1] = 1
    
    for index in range(2, num + 1):
        cache[index] = cache[index - 1] + cache[index - 2]
    return cache[num]
```

* 재귀호출보다 동적계획법으로 피보나치 수열을 구할때 속도가 빠름  
* 최하위의 해답을 먼저 구하고 상위 문제 해결   