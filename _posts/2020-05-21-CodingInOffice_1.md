---
title: "코딩잘하고싶다 - Tree"
published: false
categories:
  - CodingInOffice
tags:
  - CodingInOffice
---

## graph에서 parent node를 삭제하는데 자식노드가 존재하는 경우에 대해서 handling을 어떻게 할 것인가


1. fail 시그널을 보내준다.  

: 자식노드가 존재하므로 자식노드들이 dangling point로 나둬지도록할 수 없으니까  


2. 부모노드를 삭제하려는데 자식노드가 있다면 자식노드먼저 순차적으로 삭제한 이후 부모노드를 삭제시켜준다.  
