---
title: "[ETC] 0xff handling"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

- 0xff is the hexadecimal number FF which has a integer value of 255.
- 0xff means "the hexadecimal number ff " - in other words, the integer 255 , which has the binary representation 00000000000000000000000011111111 (when using under 32-bit integers). The & operator performs a bitwise AND operation.
- 메모리는 모든데이터를 1과0으로만 구성한 2진수로 저장
- 8개의 비트를 모아서 1Byte -> 2의 8승이며 표시 가능한 숫자의 갯수는 256가지
- 16진수표현 중 가장 큰 수인 F는 비트로 1111을 뜻하고 10진수로는 15
- 즉 8개의 비트 1111은 16진수 값으로 F에 해당하며 16진수를 표현할때는 앞에 '0x'를 붙임

```c++
byte a = ( b >>  8) & 0xff; // b is an integer
```

- The & operator performs a bitwise AND operation. a & b will give you an integer with a bit pattern that has a 0 in all positions where b has a 0, while in all positions where b has a 1, the corresponding bit value froma is used (this also goes the other way around). For example, the bitwise AND of 10110111 and00001101 is 00000101.

- In a nutshell, “& 0xff” effectively masks the variable so it leaves only the value in **the last 8 bits**, and ignores all the rest of the bits.

- It’s seen most in cases like when trying to transform color values from a special format to standard RGB values (which is 8 bits long).

- INT_MAX 2147483647
- UINT_MAX 4294967295 (0xffffffff)
- UCHAR_MAX 255 (0xff)
- [Limits on Integer Constants](https://docs.microsoft.com/en-us/cpp/c-language/cpp-integer-limits?view=msvc-170)

<!--## Code analysis (11/17)

```c++
abnormalEventPeriod = 0xff;

if(abnormalEventPeriod == 0xff) cnt++; // if cnt is equal to whole data size remove data container
```

- 굳이 0xff 를 abnormalEventPeriod 기준값으로 쓸필요가있었을까 싶은데
-->

