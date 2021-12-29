---
title: "Programming - Batch Cron"
categories:
  - Programming
tags:
  - Programming
---

### 배치
- 배치(batch)란:
    - a group of things or people that are dealt with at the same time
    - (일괄적으로 처리되는)집단, 즉 일괄적으로 뭔가가 처리되는

- 배치를 등록한다는 것은->여러가지 일을 한꺼번에 처리하기 위해 만든 프로그램
    - (매일 정해진 시간에 혹은 주기적으로 수많은 양의 작업에 대하여 명령어를 직접 타이핑 하지않고 배치 프로그램을 통해  해결)

- 이 배치를 실행하는것은 개발자가 아닌 스케쥴러가 실행하게 됨.

### 스케줄러
- 스케쥴러란:
    - 일정 주기 혹은 특정 시간에 배치 프로그램을 실행시켜주는 프로그램,
    - 리눅스에는 대표적으로 크론탭(Crontab)이 있습니다.

 
### Cron
- Cron 이란?:
    - 특정한 시간에 또는 특정 시간 마다 어떤 작업을 자동으로 수행하게 해주고 싶을 때 사용하는 명령어가 cron입니다.
    - cron은 특정한 시간에 특정한 작업을 수행하게 해주는 스케줄링 역할을 합니다.
    - 리눅스에만 있는 개념이 아닌 여러 OS에 있는 개념입니다.
    - cron 시스템에는 시스템에서 기본적으로 사용하는 cron설정이 있으며, 이를 시스템크론이라 합니다.
    - 또 root나 일반 사용자가 자신의 cron설정을 직접하여 사용하는 사용자크론이 있습니다.

- Crontab이란?:
    - cron작업을 설정하는 파일을 crontab 파일이라고 합니다.
    - cron프로세스는 /etc/crontab 파일에 설정된 것을 읽어서 작업을 수행해요
    - crontab 파일은 OS별로 각각 다른 위치에 저장이 됩니다.
    - 일반적으로 BSD계열의 리눅스는 /var/spool/cron/ID

    - 솔라리스 계열은 /var/spool/cron/crontabs/ID에 있습니다.

- anacron이란?
    - /usr/sbin/anacron 에 위치하며,
    - 크론과 같이 동작하는 프로그램으로 서버가 일정 시간 중지되었을 때에도 작업이 실행되는 것을 보장하기 위해 사용하는 도구입니다.


<!--

### batch
- Batch means:
    - a group of things or people that are dealt with at the same time
    - A group (processed in batches), that is, a group in which something is processed

- Registering a batch is a program created to process various tasks at once.
    - (Resolved through a batch program rather than directly typing commands for a large number of tasks at a fixed time every day or periodically)

- Executing this batch is done by the scheduler, not the developer.

### Scheduler
- What is Scheduler:
    - A program that executes a batch program at a certain period or at a specific time;
    - Linux has Crontab as a representative.

 
### Cron
- What is Cron?:
    - The cron command is used when you want to automatically perform a task at a specific time or at a specific time.
    - cron is a scheduling function that allows you to perform a specific task at a specific time.
    - It is not a concept unique to Linux, but a concept in many OSs.
    - The cron system has cron settings that are used by default in the system, and this is called system cron.
    - In addition, there is a user cron that root or general users use by directly setting their cron settings.

- What is crontab:
    - The file that configures cron jobs is called crontab file.
    - The cron process reads the settings in the /etc/crontab file and performs tasks.
    - The crontab file is saved in a different location for each OS.
    - In general, BSD-based Linux is /var/spool/cron/ID

    - On Solaris, it is located in /var/spool/cron/crontabs/ID.

- What is anacron?
    - It is located in /usr/sbin/anacron,
    - A program that works like a cron, and is a tool used to ensure that tasks are executed even when the server is stopped for a certain period of time.

-->