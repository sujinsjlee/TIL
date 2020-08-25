---
title: "코딩잘하고싶다 - test error detecting"
publish: false
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

- veryfyMessage 함수에서 에러가 나서 ....계속 verifyMessage 함수에서 선언된 객체의 class 를 변경하려고 애썻는데

- 테스트 코드내에서 verifyMessage함수가 호출되는부분에서 잘못된것이었음

- 그니까 에러포인트가 함수그자체가아니라 함수호출부에 있었는데!!!!

- 그리고 에러나면 좀 에러포인트를 정확히 찾고 에러분석할 것 (print 문을 걸어서 몇 번 째 line에서 나는 오류인지 확실히 체크할 것 (어디까지는 정상 동작하고 어느 포인트에서 에러시작하는지에대한 포인트 -- line detecting 이 print문이랑 컴파일러랑 다를 수 있음))
