---
title: "C++ Practice Environment"
categories:
  - C++
tags:
  - C++
---

## g++
1. [https://nuwen.net/](https://nuwen.net/)  
2. C++ MinGW Distro  
3. Download > mingw-...-without-git.exe  
	* 실행파일 눌러서 저장경로 변경
	* Extract
	* 해당 폴더로 이동
4. open-distro-window  
	* **gcc --version** : 잘 설치되었는지 체크  
```
g++ hello.cpp
a
```
`g++ hello.cpp` : 컴파일  
`g++ hello.cpp -std=c++1z` : 최신 버전의 c++14/17/20버전의 컴파일  
`a` : 실행  
	* linux 환경 : a.out  
	* window 환경 : a  
{: .notice}

## CL compiler  
1. visual studio 설치  
* visual studio 확장 문법 제거  
	* c++ standard 문법과 다르더라고 visual studio 에서 허용하는 확장문법이 있음  
	* 프로젝트 > 속성 > 언어 > 언어확장 사용안함 ( 아니오 -> 예 )  
2. CL 컴파일러 사용하기
* 시작 > 모든 프로그램 > visual studio 20xx > visual studio 20xx 용 개발자 명령 프롬프트  
* 콘솔창에서 cpp파일이 있는 폴더로 경로 이동  
	* `cl hello.cpp` : 컴파일
	* `hello.exe` : 실행  
3. cl 컴파일러 옵션  
* `cl hello.cpp /FAs` : 어셈블리 코드로 컴파일  
* notepad hello.asm : 어셈블리 코드를 메모장에서 확인 
{: .notice}