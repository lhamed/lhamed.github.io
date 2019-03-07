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
- [ ] 파이어베이스 크래시 리틱스 
  - [ ] 기존 난독화 대신 Unity APK Proguard 난독화 
   - [x] Unity Gradle Build 
      - [x] Export 해서 Android studio 에서 빌드 
      - [x] 우선은 GPGS 꼬인거 풀기
      - [x] 파이어베이스 SDK 부착 
      - [x] 인터널로 한번 빌드 (플러그인 테스트)



# 데이터 
시간 견적 정확도 : 0 hour

만족도 : 70 ( 일을 거의 못했어도 뭐.. )

목표 이행 : 70

퇴근 시 피로도 : 60

출근 시 피로도 : 90 

업무 중 생각난 아이디어의 갯수 : 0

학습량 : 2

# 업무중 학습
- Android Studio 와 Gradle 관련
   유니티 내부에서 그래들 빌드가 제대로 안된다 @_@ . 특히 커스텀 관련 부분 . 
   그리고 매핑 파일을 프린트 하는 것도 마찬가지인 것 같고 ( 방법이 있을 수도 있지만... 자료를 찾는데 실패함 )
   성공한 방법은 유니티에서 커스텀 설정 하지 않고 일단 익스포트 한 뒤에
   나머지는 안드로이드 스튜디오에서 하는 것. 

- 구글 플러그인 뗏다 붙였다 하다보면 자주 꼬이는데 , 가장 빠른 방법은 기존 플러그인을 "모두" 삭제 하고 새로 패키지를 넣는 것이다. 잔여물 있으면 엄청 꼬임 


# 내일로 미뤄진 작업 
- [ ] 기존 난독화 대신 Unity APK Proguard 난독화 
   - [ ] Gradle Proguard 빌드에서 , 유난히 씬 로딩 시간이 길어지는 이슈 디버깅 하고
   - [ ] 위 사항 해결버전 재 빌드 
- [ ] 파이어베이스 푸시 알림 SDK 구현 ( 시간이 남는 다면 ) 