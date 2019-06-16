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
- [x] 빌드
   - 버그 : GPGS 가 제대로 작동하지 않는다. 
      - [x] GPGS 를  Gradle 에서 압축하기 때문 -> 프로가드 커스텀으로 해결 . 
         - 버그 : 파이어 베이스 애널리틱스가 안된다. 
            - [x] : google-services.josn 누락 해서 다시 넣음 . ( 파이어 베이스 Configure)
- [ ] 파이어베이스 푸시 알림 SDK 구현 ( 시간이 남는 다면 ) 

# 데이터 
시간 견적 정확도 : 0 hour

만족도 : 90 

목표 이행 : 90

퇴근 시 피로도 : 80

출근 시 피로도 : 95

업무 중 생각난 아이디어의 갯수 : 0

학습량 : 4

# 업무중 학습

- 그래들 시에 로딩 시간 증가 이슈 해결법 
aaptOptions {
	noCompress 'unity3d' // or whatever extension you use
}를 그래들 템플릿에 추가 후 빌드 .

- GPGS 0.9.50 와 Firebase 5.2.0 은 호환 된다. 

- GPGS 를 압축해버리는 Gradle 을 막기 위해서 : -keep class com.google.android.gms.**{*;} 를 추가. 

- Firebase 과거 버전 다운로드 : https://dl.google.com/firebase/sdk/unity/firebase_unity_sdk_${version}.zip


# 내일로 미뤄진 작업 
] 파이어베이스 푸시 알림 SDK 구현 ( 시간이 남는 다면 )

# 궁금증
