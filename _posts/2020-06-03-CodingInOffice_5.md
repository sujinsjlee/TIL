---
title: "코딩잘하고싶다 - minor code notice"
published : false
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---


## string
```cpp
string s1;

string s2 = "";
```
- s2 처럼할 필요가 없음  
- s1에서 string 생성자가면 empty string의 객체 생성해줌  

## if 문 관련 코드 
- if 문 안에 if문 내부적으로 중첩해서 쓰는 것보다 그냥 if문 조건을 만족하지못하면 return 시키는 함수로 구현하는게 나중에 readability 도 좋음  
- 그리고 if문 안에 중첩으로 if문쓰면 추후에 관련 debug 코드가 섞여서 출력되니까 그냥 if문이 중첩되는 경우 조건만족못하면 debug 코드 출력하고 함수 return 하는 식으로 구현  