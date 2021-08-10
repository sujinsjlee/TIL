---
title: "[ETC] - code review"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---
# Code Review

<!--0219 코드리뷰 코멘트-->
## readability
<!--코드 전반적으로 readability가 떨어진다는 평가 -->

## if 문 다음에 옆에 continue 쓰고 다음 문장...쓰면 알아보기 어렵다는점
## std::all_of
<!--## 하나의 함수에서 if(!txScIdPair.empty()) 이조건 중복으로 체크하고 있는 부분 제거하는것..-->
## lambda 함수활용해서 코딩
## for 루프 하나에 로직을 다 넣을지 아니면 for 루프 두개로 개별적으로 나눌지 어떤 것이 효율적인 코딩인지..

<!--03 rpcCell 코드리뷰 코멘트-->

## errorCause 를 함수내부에 선언하고 함수파라미터 인자로 전달해서 클래스내부적으로 사용하게끔 코드 구현해놨는데 --> 이부분 errorCause를 클래스의 멤버변수로 선언하면 따로 함수 파라미터로 넘겨줄 필요없음

## errorCause를 map 타입으로 정의할 필요가 없음 --> map타입으로 정의해서 sc마다 하나씩 errorCause를 저장해놓지 말고 어차피 reponse에 실릴 errorCause는 하나니까 함수내부적으로 하나의 errorCause만 저장해놓고 Reject 시그널오면 그때 마다 condition맞춰서 errorCause 업데이트하는 형식으로 구현