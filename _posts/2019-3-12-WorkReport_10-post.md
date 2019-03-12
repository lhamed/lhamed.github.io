---
layout: post
title: WorkReport_4
description: "Fri,2019.3.4"
modified: 2019-3-4
tags: [WorkReport]
image:
  path: /images/Lawn.png
  feature: abstract-3.jpg
  credit: lhaemd
  creditlink: lhamed.github.io
---
# 오늘 목표 업무 
- [x] 푸시 관련 패치 사항 
  - [x] 푸시 중복 사용 ( 클라우드 저장 악용 버그 ) 방지 시스템 구현 
  - [x] 푸시를 받는 이벤트 핸들러가 씬 초기화를 여러번 반복하면 이상 작동하던 버그 수정 
- [ ] 신 서버 마이그레이션 

# 데이터 
시간 견적 정확도 : 0 hour

만족도 : ?

목표 이행 : ?

퇴근 시 피로도 : ?

출근 시 피로도 : 95

업무 중 생각난 아이디어의 갯수 : 0

학습량 : 2

# 업무중 학습

- C# 이벤트 핸들러는 비어 있거나 해당 이벤트가 add 안되어있어도 remove 함수는 익셉션을 뱉거나 하지 않는다.

- C# 이벤트 핸들러를 한번에 초기화 하는 방법은 없다. 
  - 하지만 리플렉션을 사용해서 인보케이션 리스틀 뽑아 가능하다. ( Unity iOS 에서 리플렉션 이상 작동하므로 쓰지 않음)


# 궁금증
