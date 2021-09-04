---
title: "MSA - Micro Service Architecture"
categories:
  - System Design
tags:
  - System Design
---

## MSA 

- 기존 시스템
    - 시스템 (인프라) 위에 APPlication (프로그램) 설치
    - **모놀릭스** 하나의 단일 APPlication / 시스템

- **MSA** : 기능별로 쪼갠다
    - micro
    - 왜..? 쪼개는 것 ?? 
        - 뭐가 좋아짐...? 
        - 쪼개지는 시스템끼리 통신가능
        - 복잡도는 올라감
        - ex 1) 넷플릭스에서 장애 발생 : 전체 서비스 다운
            - **장점1** > **전체 사이트 장애를 막자!** 
            - 일부서비스만 멈추도록
        - ex 2) 하나의 APPlication에서 여러개의 서비스를 실행중
            - service 1 : 조회
            - service 2 : 결제
            - service 3 : 정산
            - **장점2** > 만약, service 중에서 "조회" service가 전체 기능중의 API call 중의 90% 를 차지함
                - 이 경우 **인프라 측면의 효율** 관점에서 MSA 도입
                - Auto-scale 기능 도입 
            - **장점3** > **빈번한 업데이트 / 배포가 필요한 경우** 일부 service만 해당 기능만 업데이트 / 배포

- **ROI** Return of Investment 는 고려해야 (투자대비효과)

## Docker
> MSA 에서 쪼개진 각각의 service들은 Docker를 통해 개별 **image**로 관리   
> Docker에서 각각의 service들은 VM이아니라 별개의 image로 관리


- Docker : VM 과 비교했을 때 확장이 매우 쉬움

## DevOps
> MSA 에서 쪼개진 각각의 service 들은 기능 개발 / 운영 인프라 관리등의 업무로 쪼개질 수 있다  
> **DevOps : 개발 + 운영**


## SRE (Site Reliability Engineering)
>  SRE : 안정적인 site를 운영하기 위한 기술  


### Point
> 대용량 Service를 MSA구조로 가져가면서 Service Docker 기반으로 관리  
> MSA 기능단위를 DevOps 팀에서 관리 / 개발  
> DevOps 의 목표는 SRE를 고려한 안정적 / 신뢰를 갖춘  Site 운영을 목표로한다  
