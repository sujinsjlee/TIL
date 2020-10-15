---
title: "[Kubernetes] What is Kubernetes"
categories:
  - Kubernetes
tags:
  - Kubernetes
---
    
## Kubernetes  
[Kubernetes Explain](https://www.youtube.com/watch?v=S3FVcdZcZnA)  

> Kubernetes 는 컨테이너를 관리하기 위한 툴  
> 컨테이너들을 모니터링   
    - 최소 n 개의 컨테이너가 동작하도록 관리  
    - 유저가 많아진 경우 새로운 컨테이너 생성 - 웹니즈에 맞춰서 컨테이너의 수 조절  
    - 클라우드에 있는 컨테이너에 버그가 있는 경우 -> 웹사이트가 다운되는것없이 쿠버네티스가 하나씩 업데이트해줌)  

* **POD**
    * 컨테이너 집합
    * 근데 현재 1 pod 안에 1container만 있게끔함
* **kubectl** : 명령어 (Kubectl controls the Kubernetes Cluster)

* **Deployment**  

* **Label**

* **Helm**(In simple terms, Helm is a package manager for Kubernetes)
    * Kubernetes 에서 많이 쓰이는 것  
    * Kubernetes 의 Add on 기능 같은 것
    * POD 안에 깔림
