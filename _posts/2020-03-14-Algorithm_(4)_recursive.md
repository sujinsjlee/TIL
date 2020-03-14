---
title: "Algorithm - (4) 재귀 용법"
categories:
  - Algorithm
tags:
  - Algorithm
use_math: true
---

## 재귀 용법 (recursive call, 재귀 호출)  
> **함수 안에서 동일한 함수를 호출하는 형태**  
> 함수는 내부적으로 **스택**처럼 관리(프로세스 내의 스택)  

# 프로그래밍 연습 (C++)  

## 회문(palindrome) 
> 순서를 거꾸로 읽어도 제대로 읽은 것고 동일한 단어를 판별하는 함수  
> ex) level, mom  

<!--면접에 자주 출제되는 문제-->

* 회문을 **재귀 용법**으로 구현  
```cpp
#include <iostream>
#include <cstdio>
/*
l e v e l
0 1 2 3 4  len 5 size 2

m o m o
0 1 2 3  len 4 size 2 
*/
using namespace std;


bool isPalindrome(char * str_s, int s, int e)
{
	if(s == e) //one charactor
		return true;
		
	if(str_s[s] != str_s[e]) // not palindrome
		return false;
	
	if(e - s > 1) // in case of len is even
	//if( end - begin > 1 )
		return isPalindrome(str_s, s+1, e-1);
	
	return true;
}

int main()
{
	char str[100];
	scanf("%s", str);
	int len = 0;
	for(int i = 0; str[i] ; ++i)
	{
		++len;
	}
	
	printf("%d\n", len);
	
	if(isPalindrome(str, 0, len-1)) //since array index starts from 0, the -1 is essential
		cout << "the input string is palindrome" << endl;
	else
		cout << "the input string is not palindrome" <<endl;
	
	
	
	return 0;
}
```

* 회문을 **반복문**으로 구현  
```cpp
#include <iostream>
#include <cstdio>
/*
l e v e l
0 1 2 3 4  len 5 size 2

m o m o
0 1 2 3  len 4 size 2 
*/
using namespace std;


bool isPalindrome(char * str_s, int size)
{
	bool palindrome = false;
	for(int i = 0; i < size; ++i)
	{
		if(str_s[i] == str_s[size*2 - i])
		{
			palindrome = true;
		}
		else
		{
			palindrome = false;
			break;
		}
	}
	
	return palindrome;
		
}

int main()
{
	char str[100];
	scanf("%s", str);
	int len = 0;
	for(int i = 0; str[i] ; ++i)
	{
		++len;
	}
	
	printf("%d\n", len);
	
	if(isPalindrome(str, len/2))
		cout << "the input string is palindrome" << endl;
	else
		cout << "the input string is not palindrome" <<endl;
	
	
	
	return 0;
}
```


## 정수가 1이되는 과정을 출력하는 함수  
1. 정수 n에 대해
2. n이 홀수이면 3 X n + 1 을 하고,
3. n이 짝수이면 n 을 2로 나눕니다.
4. 이렇게 계속 진행해서 n 이 결국 1이 될 때까지 2와 3의 과정을 반복합니다.

```cpp
#include<iostream>
using namespace std;

void test(int n)
{
	cout << n <<endl;
	if(n == 1)
		return;
	
	if(n % 2 != 0)
		return test(3*n + 1);
	else
		return test(n / 2);

}

int main()
{
	int n;
	cin >> n;
	
	test(n);
	
}
```

## ACM-ICPC > Regionals > Asia > Korea > Asia Regional - Taejon 2001  

문제: 정수 4를 1, 2, 3의 조합으로 나타내는 방법은 다음과 같이 총 7가지가 있음
1+1+1+1
1+1+2
1+2+1
2+1+1
2+2
1+3
3+1
정수 n이 입력으로 주어졌을 때, n을 1, 2, 3의 합으로 나타낼 수 있는 방법의 수를 구하시오
{: .notice--info}

> point: 정수 n을 만들 수 있는 경우의 수를 리턴하는 함수 - f(n)  
> f(n) = f(n-1) + f(n-2) + f(n-3)  

```cpp
#include<cstdio>
#include<iostream>

using namespace std;

int test(int data)
{
	if(data == 1)
		return 1;
	else if(data == 2)
		return 2;
	else if(data ==3)
		return 4;
	
	return test(data-3) + test(data-2) + test(data-1);
}

int main()
{
	int n;
	cin >> n;
	int count = test(n);
	
	cout << count << endl;
}
```

