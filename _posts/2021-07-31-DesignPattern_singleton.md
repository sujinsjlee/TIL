---
title: "Design Pattern - Sigleton Pattern"
categories:
  - Design Pattern
tags:
  - Design Pattern
---

# Singleton Pattern
> Singleton : 클래스의 인스턴스는 **오직하나임을 보장**하며 이에대한 접근은 어디에서든지 하나로만 통일하여 제공한다.

## Singleton의 일반적인 구현 코드
- 생성자를 private에 놓는다.
- static 멤버 함수를 통해서 오직 하나의 객체를 생성한 후 참조를 반환한다.
