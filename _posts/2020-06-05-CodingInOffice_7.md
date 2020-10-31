---
title: "[ETC] - code에대해서 받은 comment들"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---
<!--코딩잘하고싶다-->

## Doxygen comment 
- Add some short descriptive comment (preferably doxygn format) on what it does and what it returns  
- Doxygen comment in C++ should be before the method declaration, unlike in Python :)  

## Readability
- Can't say for sure since it's a bit hard to reveiw code not using a proper editor, but I guess that there is a lot of duplicated code in this file.  
Perhaps start looking if this can be extracted. I think it would increase readability.  
	- need to add comment for readability and understanding for other developer.  

## Function parameter
- could this method take CmService, gnbCuUpFunctionLdn as args instead?  
- [함수 파라미터에 const를 붙여야하는 경우](https://hashcode.co.kr/questions/406/%ED%95%A8%EC%88%98-%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0%EC%9D%98-const%EB%8A%94-%EC%96%B4%EB%94%94%EA%B9%8C%EC%A7%80-%EB%B6%99%EC%97%AC%EC%A4%98%EC%95%BC-%ED%95%A0%EA%B9%8C%EC%9A%94)  
- 구조체 포인터  
https://stackoverflow.com/questions/15181765/passing-structs-to-functions 
https://stackoverflow.com/questions/2724708/is-it-a-good-practice-to-pass-struct-object-as-parameter-to-a-function-in-c 
https://stackoverflow.com/questions/10370047/passing-struct-to-function 

## 멀티 스레드
c++ extern 키워드 스레드
http://www.jiniya.net/ng/2016/11/magic-statics/
 
## 변수선언
- 두번이상 함수의 return 값을 활용하는 경우가 있다면 그냥 변수 선언을 하는게 좋음  

## 함수 STL 사용할 때 조심할 점_ return 값이 reference값을 가져오는 경우를 조심하자!!
- string stl을 사용할 때 반드시 주의할 것!!
	- ip 주소마다  마지막 주소값이 달라서 string stl의 back() 함수를 이용했는데  
	- back() 함수는 reference로 return값을 넘겨줌  
	- 만약에 back() 함수의 return 값을 그냥 if문에서 체크하는게 아니라 back() 값을 바꾸는 코드가 들어갔다면 reference값이니까 값이 바뀌었겠죠? 이런 점에대해서 항상 stl 함수사용할 때 주의할 것  
	- 참고로 front() 함수도 값 return해줄 때 reference값을 넘겨줍니다.  


## Boolean varaiable_naming
- Rename the variable to something saying what it is sued for, for example:
- __is__Created
- __should__Created 

## variable declare as auto*
- auto*  
- c++에서 auto 란 무엇인가  


## Finding Error
> 컴파일에러가 아닌 런타임 에러 찾기  


- 우선 에러를 마주하면 에러가 발생한 코드 앞전뒤후로 분명히 에러가 있음  
- 따라서 에러가 발생한 시점부터 전에 작성한 코드는 모두의심하고  
- 특히 에러포인트 전에 에러가 난 포인트의 변수는 어떤 타입으로 선언된건지  
- 변수는 올바른 타입으로 선언된건지  
- 범위 체크는 잘 된 것인지
<!-- 에러가 함수 내의 transaction을 apply하는 부분에 서 에러남
그러면 apply가 안되니까 modifyTransaction, deleteTransaction이 하나에 있었는데  이걸 쪼개볼까..? 에대해체크했고
쪼개고나서도 에러가 났는데 그러면 modify에서 에러가났는데 그러면 modify하는 부분에서 내가 변수선언을 잘못했나보다
modify쪽에서 변수선언 잘못했었음-->
