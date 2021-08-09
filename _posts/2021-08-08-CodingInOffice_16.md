---
title: "Programming - Understanding Makefile"
categories:
  - CodingInOffice
tags:
  - CodingInOffic
---

## Makefile
> **Makefile**  
> 반복되는 컴파일 작업의 시간을 줄이기 위해 수정된 파일만 컴파일 할 수 있게 함  
> 대규모 프로젝트, 공동 프로젝트에서 반드시 필요  

## Compile과정
- 1. **소스파일 .c**
  - 개발자가 이해할 수 있는 프로그래밍 언어로 이루어진 파일 
  - .c  / .cpp 파일
- 2. **목적파일 .o**
  - 소스파일을 컴파일러가 기계어로 변환한 파일
  - .c 파일을 .o파일로 바꾸는 과정을 **컴파일**한다고함
  - 컴파일러에 의해서 오브젝트 코드로 저장된 파일은 기계어 (Binary) 코드로 변환되어있음
- 3. **실행 파일 a.out**
  - 기계어로 이루어진 목적파일(.o)에 라이브러리 파일(.a)을 Linking 해서 만든 실행 파일
  - unix (a.out)
  - window (a.exe)


## Makefile

```makefile
TARGET : DEPENDENCY
  command
```

- TARGET 을 만드려면 DEPENDENCY가 필요함
- tab +command : command명령을 입력하면 TARGET을 만들 수 있음


```console
~$ vi Makefile
```



```console
CC = gcc
TARGET = app.out
OBJS = main.o kor.o usa.o

CFLAGS = -Wall
LDFLAGS = -lc

all : $(TARGET)

$(TARGET) : $(OBJS)
  $(CC) $(LDFLAGS) -o $@ $^

.c.o : 
  $(CC) $(CFLAGS) -c -o $@ $<

/------------------
main.o : 
  $(CC) -c main.c

kor.o : 
  $(CC) -c kor.c

usa.o : 
  $(CC) -c usa.c
```

- **all** 옵션이 없는 경우 제일 첫번째 Target 만 실행시키고 종료

- `$@` : TARGET
- `$^` : DEPENDENCY
- `$<` : TARGET 을 .c라는 source file로 잡아주겠다
- `CFLAGS` : compile option 
  - w : warning
  - wall : all warning
- `LDFLAGS` : Linking option 
  - lc : c library


```console
~$ make
gcc -c main.c
gcc -c kor.c
gcc -c usa.c
gcc -o app.out main.o kor.o usa.o

~$ 
```
