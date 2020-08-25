---
title: "C++ - String to Int/ Int to String"
categories:
  - C++
tags:
  - C++
link:
---

# BOJ 5430 문제 풀이

## Reverse 함수 구현
컨테이너 내부 원소를 reverse 하라는 명령이 들어온다고 진짜로 배열의 모든 원소를 뒤집으면 절대로 안 됩니다.  
N개의 원소의 순서를 정말로 바꾸면 당연히 그 원소 수만큼 시간이 걸리고, 그걸 최대 10만 번 수행해야 하니 테스트 케이스 1개만으로도 100억번의 연산이 수행됩니다.  
**Reverse 명령의 핵심은 실제로 원소를 뒤집지 않고도 뒤집힌 것과 같은 효과를 내도록 구현하는 것입니다.**  
 
C++의 std::reverse(), Python의 a[::-1] 역시 사용해서는 안 됩니다.
```cpp
if(order == 'R') 
	isReverse = !isReverse;
				
if(!isReverse) {
	cout << "[";
	while(dq.size() > 1) {
		cout << dq.front() << ",";
		dq.pop_front(); 
	}
	cout << dq.front() << "]\n";		
	
}
else {
	cout << "[";
	while(dq.size() > 1) {
		cout << dq.back() << ",";
		dq.pop_back(); 
	}
	cout << dq.back() << "]\n";		
}				
```

**DEQUE 의 front(), back() 함수를 통해서 reverse flag bool type에 따라서 deque 에서 연산을 front()로하거나 back()으로 원소에 접근**

## String to Int
```cpp
string arr;
cin >> arr;
int x = 0;
for(int i =0 ; i <arr.size(); i++) {
	if(arr[i] == '[')
		continue;
	else if('0' <= arr[i] && '9' >= arr[i]) {
		x = x*10 + (int)(arr[i]-'0');
	}
	else if(arr[i] == ',' || arr[i] == ']'){
		if(x > 0)
			dq.push_back(x);
		x = 0;
	}				
}
```
- int value = **(int) c - '0'**;
	- c 데이터가 char 타입일때 int로 강제형변환 하여 '0' 을 빼주면 c에 해당하는 int 값을 구할 수 있다.

```cpp
const char *str2 = "3.14159";
int num2 = std::atoi(str2); 

std::string str1 = "45";
int myint1 = std::stoi(str1);
```

- atoi() : char형 문자열을 정수형태로 변환  

- stoi() : string 데이터타입의 문자열을 정수형으로 변환  


## Int to String
- to_string()

```cpp
double f = 23.43;
std::string f_str = std::to_string(f); 
```

