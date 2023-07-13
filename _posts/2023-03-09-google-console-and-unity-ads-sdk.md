---
layout: post
title: 구글 콘솔 "앱에 규정을 준수하지 않는 SDK 버전이 포함되어 있습니다"
description: 
modified: 2023-03-09
tags: [Unity,Google,PlayStore]
image:
  credit: lhaemd
  creditlink: lhamed.github.io
---

# 이슈 

구글 콘솔에 다음과 같은 메세지를 받았다. 

>2022년 12월 22일 02:02
>com.betdon.egosword 앱 버전 코드 1867에 개인 정보 또는 민감한 정보를 수집하면서도 Advertising ID, Android ID 식별자로 제한되지 않는 com.unity3d.ads:unity-ads SDK 또는 라이브러리 중 하나가 사용하는 SDK가 포함되어 있습니다. 데이터 사용 정책에 설명된 것과 같이 영구 기기 식별자는 다른 개인 정보 및 민감한 사용자 데이터 또는 재설정 가능한 기기 식별자와 연결될 수 없습니다.
>2023년 1월 11일 자정(UTC)부터 사용자 데이터 정책을 준수하지 않는 SDK 버전이 포함된 새로운 앱 출시 버전은 출시에서 차단될 수 있습니다. SDK 제공업체에서 제공하는 경우 정책을 위반하는 코드가 포함되지 않고 정책을 준수하는 버전의 SDK로 업그레이드하거나 앱에서 이 SDK를 삭제하는 것이 좋습니다.
>SDK 제공업체에 따르면 4.0.1 버전으로 업그레이드하거나 SDK 제공업체에 문의하여 적합한 이후 버전을 사용할 수 있는지 확인하는 것이 좋습니다. Google은 서드 파티 소프트웨어를 보증하거나 추천할 수 없습니다.
>조치 필요: 정책을 준수하는 새 버전을 업로드하고 정책을 준수하지 않는 버전을 비활성화하세요.
>자세한 내용은 사용자 데이터 정책을 참조하고, 검토를 위해 업데이트된 앱을 제출하는 방법은 여기에서 확인하세요.
>정책을 검토한 후 Google의 결정이 잘못되었다고 생각되면 정책 지원팀에 문의하시기 바랍니다.

# 공식 답변

https://forum.unity.com/threads/your-app-includes-non-compliant-sdk-version.1302498/


# 문제의 핵심 

다음은 유니티가 구글과 논의해 공식적인 답변을 인용한다. 

> The notice should have the specific version where they detected the non-compliant SDK.
> You'll need to deactivate/remove any uploaded builds with older SDK versions.


# 결론 

새 광고 SDK를 붙이고, 기존 빌드를 de-activate 하는 것으로 이슈 클로징 될 것으로 보인다. 
만약 문제가 있다면 돌아와서 기록을 수정하겠다.


