---
title: "[Docker] What is Docker"
categories:
  - Docker
tags:
  - Docker
---

## Docker
[Docker explain](https://www.youtube.com/watch?v=chnCcGCTyBg)  
[Docker start](https://docs.docker.com/get-started/)  

`neeed to check the comparison between VMware and Docker`  
* VM ware : 하드웨어의 가상화시키는 기술  
* Host OS : 리눅스 os  
* Docker : OS 를 가상화 시키는 기술?? 근데 퉁쳐서 이렇게 볼 수는 있는데 리눅스에 컨테이너를 여러개만들어서..동작하게끔  
* Container : OS 에 namespace를 이용해서   
* Namespace : 
    * 직역하면 이름공간, 의역하면 소속이라 해석됨
    * 커널 자원들을 구분해서 이를 프로세스에 제공해 그 프로세서의 소속된 자원처럼 구분함
    * 프로세스 테이블, ipc, 네트워크(IP 주소, 방화벽등), User ID, 마운트 포인트 등을 가상화
        * ex ) 네트워크를 namespace를 부여해서 독립적으로 관리하기 위해 ~~  
    * [setns](https://man7.org/linux/man-pages/man2/setns.2.html)

> docker는 **environment disparity**라는 문제점을 해결  
> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers.  

- docker를 통해 다른 머신에서도 같은 환경을 구현할 수 있음  

1. 윈도우와 서버에 docker를 모두 설치하도록한다  
2. docker파일 생성 (docker 파일에 내가 구현하고 싶은 환경을 설정하면됨 - ex: ubuntu,python,git)
3. docker파일을 서버와 컴퓨터에 모두 줌
4. docker는 그 파일을 읽고 필요한 것을 다운로드 받음
5. docker는 해당 설정한 환경과 같은 virtual container(ex: ubuntu,python,git)를 컴퓨터에 만들어 놓음
6. 그래서 내가 컴퓨터에서 서버로 코드를 업로드할때 (docker 파일과 함께) --> 잘 작동하게 된다
7. docker 컨테이너들은 각기 분리되어있다고 생각됨 --> 따라서 한개의 서버에 각기다른 수많은 컨테이너를 가질 수 있음

- docker의 장점
    - docker덕분에 매번 새로운 서비스를 만들 때마다 새로운 서버를 사고, 설정할 필요가 없음
    - 내가 원할때 마다 docker를 통해 새로운 환경을 생성할 수 있음
    - 서버를 사고, 환경을 설정하고, 시작하고..를 반복할 필요가 없음
    - 그냥 컨테이너를 생성하고 복제하면됨 (원하는 만큼)
    - **하나의 같은 서버에서 각기다른 환경의 컨테이너를 설정할 수 있고 이 컨테이너들은 각각 분리 독립되어 있음**


> * 원하는 개발환경을 파일에 저장하면, docker는 이를 너가 원하는 어떤 머신에든 해당 환경을 시뮬레이션 해준다.
> * 이러한 환경들이 각기 독립적으로 존재하기 때문에, 원하는 무슨 환경이든 모듈식으로 관리가능하다!


* **alpine**  
    * docker 에서 돌아가는 가작 작은 OS  

* **DevOops**
    - 개발자가 이미지를 만들어서 docker에 배포를 해두면 run만 한번하면 launching 시킬 수 있는 것
    - Development + Oops : Docker랑 kubernetes 를 이용해서 일하는 것

* 참고 ) 0.0.0.0 : 모든 IP주소를 의미 

* **IMAGE**
    * 이미지는 컨테이너 실행에 필요한 파일과 설정값등을 포함하고 있는 것으로 상태값을 가지지 않고 변하지 않습니다.
    - Layer라는 개념을 사용하고, 유니온 파일 시스템을 이용하여 여러개의 레이어를 하나의 파일 시스템으로 사용할 수 있게 해줍니다.  
