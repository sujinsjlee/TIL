---
title: "C++ - Vector index 접근 / 수정 / 삭제"
categories:
  - C++
tags:
  - C++
link: https://sujinsjlee.github.io/c++/2020/10/19/C++_vectorStl/
---

# ABOUT Vector index

## vector index value 수정
> **at** : access specified element with bounds checking  
> **operator[]** :  access specified element  



```c++
vector <int> v;
for(int i=1;i<=10;i++){
   v.push_back(i);
}

v.at(4) = -1;
v[4] = 77;
```
- `at` and `operator[]` both return a reference to the indexed element

-  you'd better take the habit to use `at`, less idiomatic, but bound-checking is priceless

- A much better way is to use `at(...)`. This will automatically check for out of bounds behaviour and break throwing an **std::out_of_range**. So in the case when we have
```cpp
v.at(10) = 9;
```
- We will get:  
terminate called after throwing an instance of 'std::out_of_range'
what(): vector::_M_range_check: __n (which is 10) >= this->size() (which is 4)

- `at()` 을 쓰는게 좋겠네요. code test 에서 vector로 컨테이너 구현하고 [] 인덱스 접근했더니 시간초과 에러났었음. 앞으로 `at()`을 쓰도록 합시다  

## vector - erase : 데이터 삭제

```c++
vector <int> v;
for(int i=1;i<=10;i++){
   v.push_back(i);
}

int count = 0;
for(vector<int>::iterator it = v.begin(); it != v.end(); it++){
    if(count == 5){//index가 5이면 데이터를 삭제
        it = v.erase(it);
        break;
    }else{
        count++;
    }
}
```


## vector - insert : 데이터 추가

```c++
vector <int> v;
for(int i=1;i<=10;i++){
   v.push_back(i);
}

int count = 0;
int i = 0;
for(std::vector<int>::iterator it = v.begin(); it != v.end(); it++){
    if(count == 5){//index가 5이면 데이터를 추가
        v.insert(it,6);
        break;
    }else{
        count++;
    }
}
```
