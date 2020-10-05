---
title: "[ETC] - code review"
categories:
  - CodingInOffice
tags:
  - CodingInOffice
publish: false
---
# Code Review

## 예외 케이스 코드 고려
- Consider in which states the message can be received and specify an action for them if needed.  
- E.g. can we be sure that it cannot be received in LOCKING? An operator can probably lock when a message is already incoming. We also have mechanisms that automatically lock/unlock cells (when a PrepareForBfnAdjustmentReq is received for example).

## test코드에서 변수 type이 너무 긴 클래스 이름인 경우 type을 auto로 할 것
- auto

