---
title: "[Clean Code] Chapter 5: Formmating"
categories:
  - Clean Code
tags:
  - 노마드코더
  - 북클럽
  - 노개북 
---

# DAY5 : Chapter5 Formmating
#### 오늘읽은 범위: ~ 5장.형식맞추기 
- Formatting 은 의사소통이다. 의사소통은 전문개발자의 일차적인 의무다.
- **Code formatting is important. Code formatting is about communication, and communication is the professional developer’s first order of business.**

## 책에서 기억하고 싶은 내용

> **Formatting : 팀규칙. 프로그래머라면 각자 선호하는 규칙이 있다. 하지만 팀에 속한다면 자시니 선호해야할 규칙은 바로 팀 규칙이다.**  

- 신문기사처럼 작성하라 : 간결하고 짧게  
- 새로운 concept마다 줄바꿈하라
- 서로 밀접한 개념은 세로로 가까이 둬야한다
    - 변수선언 : 변수는 사용하는 위치에 최대한 가까이 선언
    - 인스턴스 변수 : 인스턴스 변수는 클래스 맨 처음에 선언
    - 종속함수 : 한 함수가 다른 함수를 호출한다면 두 함수는 서로 세로로 가까이에 배치
    - 개념적으로 유사한 함수 : getValueA, setValueA 드 명명법이 똑같고 기본 기능이 유사한 경우 가까이 배치
- 호출되는 함수를 호출하는 함수보다 먼저 배치
- 가로길이, 행은 짧을수록 좋다
- Indentation 들여쓰기 : 간단한 if문, 짧은 while문이더라도 모든 코드에서 Indentation은 가독성을 높인다


## 소감
- 일관적인 formatting style은 team의 legacy code rule을 따르는 것

## 궁금한 점 
- 밥아저씨 Uncle Bob 
    - Robert C. Martin, colloquially called "Uncle Bob", is an American software engineer, instructor, and best-selling author. 
    - Uncle Bob teaches the basics of Clean Code as described in the Clean Code book.
    
`#노마드코더`  
`#북클럽`  
`#노개북` 
