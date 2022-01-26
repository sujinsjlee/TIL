---
title: "Programming - Canary Deployment"
categories:
  - Programming
tags:
  - Programming
---

## Canary Release; Canary Deployment; Canary Development, Canary Test
> 아주 작은 변경사항만 적용하고 문제가없으면 버전을 적용  
> 조금씩 조금씩 배포하는 것  
> Canary deployments are a pattern for rolling out releases to a subset of users or servers. The idea is to first deploy the change to a small subset of servers, test it, and then roll the change out to the rest of the servers.  

- 안정적인 버전을 릴리즈하기 전에 테스트버전을 일부 사용자에게 배포하는 것
- 카나리 버전에 심각한 버그가 발생된다고 해도 사용하는 사용자가 적기 때문에 피해 최소화 가능

- 안정적인 버전과 테스트 버전이 모두 배포된 상태이기 때문에 A/B 테스트, 블루그린 배포 가능
    - **a/b 테스트**는 기존서비스 A와 새로적용하고 싶은 서비스 B를 통계적인 방법으로 비교하여 새로운 서비스가 기존 서비스에 비해 정말 효과가 있는지를 알아보는 방법
    - **Blue-Green 배포**는 애플리케이션 또는 마이크로서비스의 이전 버전에 있던 사용자 트래픽을 이전 버전과 거의 동일한 새 버전으로 점진적으로 이전하는 애플리케이션 릴리스 모델 (이때 두 버전 모두 프로덕션 환경에서 실행 상태를 유지)
        - 이전 버전을 blue 환경으로, 새 버전은 green 환경으로 부를 수 있습니다. 프로덕션 트래픽이 blue에서 green으로 완전히 이전되면 blue는 롤백에 대비하여 대기 상태로 두거나 프로덕션에서 가져온 후 업데이트하여 다음 업데이트의 템플릿으로 삼을 수 있습니다.

 