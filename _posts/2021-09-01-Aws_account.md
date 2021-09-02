---
title: "AWS - 회원 가입 / 보안설정(MFS - 2단계인증)"
categories:
  - AWS
tags:
  - AWS
---

> [생활코딩](https://opentutorials.org/course/2717)

- 회원가입
    - 외부 서버 프로그램이기때문에 평소에 잘 사용하지 않는 PASSWORD 사용을 권장
    - visa 카드등록 
    - 전화번호 등록
    - 계획지원 : AWS 문제 공식적으로 지원받을수있는 서비스 (**기본** 선택)

    - 콘솔에 로그인 --> email / password 입력

> **MFS** : *Multi-factor authentication*

- 서버는 보안이 중요합니다. 
    - 보안을 강화하기 위한 방법으로 2단계 인증을 추가
    - **Security & Identity > Identity & Access Management** 탭 선택
        - Security Status
            - **Activate MFS on your root account** 선택
                - MFA : 2단계인증
                - **a virtual MFA device** 선택 > NEXT Step
        - 핸드폰의 AppStore > **Google OTP** 설치
        - 설정시작하기 > 제공된 키 입력하기 or 바코드 스캔
        - 핸드폰에서 주어지는 Password 를 순서대로 Authentication Code 1,2 에 입력 > **Activate Virtual MFA** > Finish

    