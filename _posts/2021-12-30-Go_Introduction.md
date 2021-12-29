---
title: "Go - Introduction"
categories:
  - Go
tags:
  - Go
---


# Go

## Introduction
> C++의 복잡함과 긴 컴파일 시간을 줄일 수 있는 간결한 언어, 또한 사용자가 배우기 쉬운 언어를 만들어보자는 취지  
> Go 언어는 컨테이너와 클라우드 환경 구축에 없어선 안될 도커(Docker) 및 쿠버네티스(Kubernetes)를 비롯해 이더리움(Ethereum) 블록체인의 메인 클라이언트 Geth의 개발에 사용되는 등 성능과 안정성을 인정받으며 시장 입지를 다지고 있습니다.

## Go > Designed by
- Ken Tompson
    - Known for : UNIX, C Programming lang
- Robert Griesemer
- Rob Pike
    - Known for : UTF-8



## Featrues 

### Concurrency
### Parallelism

> 1. 정적 타입, 강 타입 => 안정성  
> 2. 컴파일 언어 / 빠른 컴파일 속도  
> 3. 가비지 컬렉션으로 메모리 관리가 쉬움  
> 4. 병행성  
> 5. 멀티 코어 환경 지원  
> 6. 모듈화 및 패키지 시스템  

1. 안정성, 정적/강 타입
    - 정적 타입 ; 파이썬과 달리 C언어처럼 int a=1 방식으로 자료형을 정적으로 선언한다.
    - 강 타입 : 약 타입은 값의 자료형을 바꿀 수 있고 강 타입은 자료형을 바꿀 수 없음을 의미한다.
2. 컴파일 언어, 빠른 속도
    > **빠른 속도**  
    > 종종 개발 스피드와 기계 스피드 needs compromise  
    > * `c++` : low development speed / fast execution speed(컴파일언어라서 코딩이끝나면 0,1로 변환 --> 이는 기계와 가까워서 실행속도가 빠름)   
    > * `python`: fast development seeped / low execution speed  
    > * **Go** : fast development spped / fase execution speed  



    - 컴파일 언어 : 기계어로 번역해 실행파일로 만드는 언어, 전처리-컴파일-어셈블-링크 과정을 거친다.
    - 컴파일 언어 종류 : C, C++, C#, Go
        - 인터프리터 언어 : 
            - 프로그램 소스코드를 바로바로 실행하는 언어
            - 느리지만 최근은 실행 시점에 컴파일하는 JIT 컴파일러 방식이 등장했다. 그래도 느리다.
            - 인터프리터 언어 종류 : 파이썬, 루비, 펄, php, 자바스크립트
        - 고 언어는 컴파일 언어인 동시에 C와 달리 헤더가 아닌 패키지 개념을 사용해 컴파일 속도가 빠르다.
        - 패키지 개념을 사용하면 사용하는 부분만 어셈블하니까.

3. 가비지 컬렉션
    - C언어는 메모리를 할당하면 반드시 해제하는 과정이 필요하며 가비지 컬렉션을 지원하면 알아서 해줘서 해당 과정이 필요가 없다.

4. 병행성
    - 동시 처리 개념이다. 고 언어의 루틴을 통해 쓰레드를 생성해 실행한다. 병행성을 이용하면 프로그램이 서로 소통하는 동시성 프로그램을 만들 수 있다.

5. **멀티코어 환경 지원**
    > 멀티코어 프로그래밍(Multi-core programming)이란 하나의 작업을 위해 여러 개의 CPU 코어를 사용하기 위해 코드를 작성하는 작업을 말한다


    - Nowadays, computers have multi-core processor and Go is built for that
    - Making application with Go 
        - use multi-core processing 
        - use parallel processing
    
6. 모듈화 및 패키지
    - 코드의 재사용을 위한 모듈화 시스템, 인터넷을 통해 패키지 사용 가능

## Difference with C
- Go 언어는 C와 구문은 비슷하지만 복잡도를 낮추고 컴파일 속도 향상을 위해 기존에 사용하던 헤더 파일을 정의하는 방식 대신 소스 자체를 패키지화하는 방식을 채택했습니다. 소스 코드 자체를 패키지화하여 변경된 부분만 컴파일 함으로써 컴파일 속도를 향상시켰습니다.

- 또한 Go 언어는 소스 내에 사용하지 않는 변수나 패키지가 있을 경우 컴파일 시 오류를 발생합니다. 불필요한 패키지 가져오기에 따른 지연 시간을 줄이고 사용하지 않는 변수 및 패키지 선언으로 인해 향후에 발생할 수 있는 버그를 줄이고자 함입니다.

## 동시성 (Concurrency)
- Go 언어는 시스템 프로그램, 특히 서버 개발용으로 설계되었습니다. 기존에 서버 개발에 널리 사용되던 C, C++, Java는 멀티 코어, 네트워킹 및 웹 애플리케이션 개발이 활발히 이뤄지기 전에 만들어진 언어들이라 사용하기 어렵거나 기능이 제한적이었습니다. Go 언어는 이러한 클라이언트가 있는 웹 서버를 실행하는 멀티 코어 환경에 맞추어 쉽게 프로그래밍할 수 있도록 고루틴(goroutine)과 채널(channel)을 제공합니다. **고루틴**은 Go 런타임에서 관리되는 일종의 경량 스레드이며 채널을 통해 고루틴 간에 메시지를 주고 받을 수 있는 매커니즘을 제공합니다. 고루틴과 채널을 활용해 멀티 코어 환경에서 병렬처리를 쉽게 구현할 수 있습니다.
- 고루틴은 자체 Go 런타임 스케줄러에 의해 관리되며 OS 스레드에 비해서도 경량입니다. OS 스레드를 생성하는데 필요한 메모리가 1MB인 반면, 고루틴은 2KB입니다. 또한 일반 스레드와 달리 메모리의 스택 영역을 사용하며 자체 스케줄러에 의해 관리하므로 컨텍스트 스위칭 비용을 줄입니다. 여기에 Go 런타임에서 사용하는 CPU 코어 수를 지정하는 환경 변수 GOMAXPROC를 지정함으로써 병렬적으로 고루틴을 실행할 수 있습니다. 하나의 프로세스에서 보통 1만개의 고루틴을 실행시킬 수 있으며 몇십만 단위의 고루틴도 실행 가능하도록 스케줄러가 구현되어 있습니다.(스택 메모리가 부족하면 힙영역까지 확장)

## 에러처리, 함수흐름 제어
- Go 언어는 에러 처리에 있어서 기존의 try-catch-finally 형식이 코드가 복잡하고 읽기 어려워진다고 판단했습니다. 기존 C, C++은 반환되는 값 하나만으로 에러 케이스를 분석하고 그에 따른 조치를 취해야 했기에 흔히 발생하는 에러 케이스를 공통 모듈화 하는 과정에서 상세 정보가 누락되는 일도 많았습니다.

- Go 언어에서 함수는 복수 개의 값을 반환할 수 있습니다. 이를 통해 에러가 발생했을 때 일반적인 리턴과 함께 오류 메시지를 반환할 수 있고 이 기능은 에러 처리를 쉽게 합니다.

- 복수 개의 반환을 통해 에러를 감지하더라도 어떤 에러는 발생할 경우 더 이상 프로세스가 실행되는 것이 의미가 없어질 수 있으며 이 때 Go 언어는 패닉(panic)을 발생시켜 에러 후 종료하는 것을 권고합니다. 프로그램이 패닉을 만나면 현재 함수의 실행을 즉시 중지하고 실행 중인 스택 상의 고루틴을 하나씩 종료합니다. 고루틴이 모두 종료되면 최종적으로 프로그램이 종료됩니다. 단, 고루틴 내에서 발생한 에러에 대해 조치 후 정상 복구가 가능한 경우에는 고루틴 종료 전에 호출되는 recover 함수에 조치 사항을 정의함으로써 프로그램 자체를 종료하지 않고 정상 재개할 수 있습니다.
- recover문과 비슷하게 Go 언어의 defer문은 함수가 종료되기 직전에 수행되는 문장으로 함수 내에서 사용한 리소스 반환 처리와 같은 상황에 유용합니다. 사용되는 리소스를 생성하고 defer문으로 반환 처리를 예약하면 이후에 생길 에러 상황에서 프로그램이 종료되더라도 리소스 해제 누락을 막을 수 있습니다.

    ```go
    f, err := os.Open(filename)
        if err != nill {
            return "", err
        }
        defer f.Close()
    ```

## Resources
- Start with basics first:
    - [How to Write Go Code](https://golang.org/doc/code.html)
    - [Convenient way to learn go also to use this Go by Example site](https://gobyexample.com/)
- And try your own code using the online playground: 
    - [Then move to advanced stuff](https://golang.org/doc/effective_go.html)
    - [There is also nice page that collects all the common practices. Very useful](https://github.com/golang/go/wiki/Cod) 
    - [And here is another one for all the gotchas](http://devs.cloudimmunity.com/gotchas)

- And last but not least, you can always refer to the language spec. It is good source of truth: 
    - https://golang.org/ref/spec