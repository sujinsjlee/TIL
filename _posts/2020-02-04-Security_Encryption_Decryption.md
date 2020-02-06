---
title: "암호화 복호화"
categories:
  - Security
tags:
  - Computer, Security
published: false
---
[노마드 코더 - 암호화](https://www.youtube.com/watch?v=67UwxR3ts2E)

## 패스워드 시스템
1. 유저는 회사에서 주는 key로 로그인  
* 암호를 해제하고 패스워드가 맞으면 로그인! 로그인이후로 다시 패스워드는 암호화  
* key를 훔치게 되는 경우에는 안좋은 방법  
2. hash함수  
* hash함수를 이용한 패스워드 시스템
	* hash함수는 동일한 입력값에 대한 동일한 출력값을 가지고 있음  
* hash함수로 암호화된 해쉬값을 비밀번호로 데이터베이스에 저장
* 일반적으로 해쉬값은 암호화되어 password를 알 수 없지만 **Rainbow table**에서 해쉬값에 매칭되는 입력값을 알려줌  
	* [Rainbow_table](https://en.wikipedia.org/wiki/Rainbow_table)  
* 그래서 **Salt** 가 등장  
	* [Salt](https://en.wikipedia.org/wiki/Salt_(cryptography))  
	* salt는 작은 랜덤 데이터고 이 salt와 함께 입력값을 해쉬함수에 전달하면 Rainbow_table 를 이용하는 해커로부터 패스워드를 지켜낼 수 있음  
{: .notice}

## 암호화  
Encryption 
* 암호의 종류  
	* 대칭키 암호화 방식  
	* 비대칭키 암호화 방식  
	* 해싱  
{: .notice}

## 복호화  
Decryption  
{: .notice}

## 암호화 해시함수  
[암호화 해시함수](https://ko.wikipedia.org/wiki/%EC%95%94%ED%98%B8%ED%99%94_%ED%95%B4%EC%8B%9C_%ED%95%A8%EC%88%98)  
* MD5, SHA-1, SHA-2, SHA-256  
{: .notice}

## 메시지 인증 코드 
[메시지 인증 코드](https://ko.wikipedia.org/wiki/%EB%A9%94%EC%8B%9C%EC%A7%80_%EC%9D%B8%EC%A6%9D_%EC%BD%94%EB%93%9C)  
* MAC (Message Authentification code)   
{: .notice}