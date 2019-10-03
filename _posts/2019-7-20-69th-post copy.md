---
layout: post
title: 일정 시간이 지나면 보상을 주는 컨텐츠 기능 설계 
description: 
modified: 2019-7-20
tags: [ Unity , GameDev, Function ] 
---

## 서문

젠킨스도 사내 개발 프로세스에 잘 정착 되었다. 

64 Bit 프로세서 지원과 그걸 위한 IL2CPP 로 백엔드 스크립트 전환하는 작업으로 또 2주를 보냈다. 

역시 잘 마무리 되었으니, 슬슬 새 컨텐츠. 

방치형 게임에서는 아무래도 그 이름 그대로 방치를 해두는 컨텐츠가 대부분이다.

문제는 이 방치를 공정하고 오차 없이 측정하는 데에 있다. 

게임을 켜둔 것이야 뭐 적당히 메모리해킹 막고 서버 시간을 받아오는 등의 노력으로 막을 수 있겠지만, 

문제는 게임을 꺼두었을 때도 , 인터넷이 되지 않을 때에도 방치 보상은 그에 맞게 주어져야 한다는 데 있다. 

거기에 기기 타임은 손쉽게 바꿀 수 있으니 , 또한 여러 국가를 다니는 유저는 악용할 마음이 없더라도 

시간축이 계속해서 바뀌니, 기기 시간을 받는 것은 여러모로 위험한 선택이다. 

## 기능 명세 

- 유저가 요청 한 시간 이후 일정 시간이 지나면 보상을 받는다.

- 만약 경과시간이 기준치를 초과 하면 보상 최대치 이내에서는 초과한 비율만큼 보상을 더 받는다. 

- 게임을 종료하더라도, 경과 시간은 측정되어야 한다. 

- 앱을 중지하더라도 ( 퍼즈 상태 , 백그라운드 상태 ), 경과 시간은 측정되어야 한다. 

- 사내 서버 이용은 최소화 한다. 

- 기기 시간의 조작이나 메모리 해킹에서 자유로워야 한다. 

- 인터넷 통신을 최소치로 유지하는 것이 좋다. 

- 스피드 핵에서도 안전해야 한다. 

## 논의

### 1.경과시간 

물론 , 블록체인에서 POW 해쉬 알고리즘 처럼 , 계속해서 연산을 해서 시간의 경과를 알아내는 방법도 있겠지만, 

상기 기능 명세를 잘 보면, 시간의 경과를 지속적으로 더하는 개념이나 가산으로 판단하는 것은 굉장히 피곤해 질 것임을 알 수 있다. 
_(게임을 종료하거나, 중지만 해도 뻔하다. ))_

잘 생각해보자. 

> 경과시간 = (종료 시 측정한 Unix Time)) -- (시작 시 측정한 Unix Time))

고등학교 물리에서 자주 등장하던 아주 아주 기초적인 정의이다.

따라서 우리는 경과시간을 직접 측정하기 보다는 다음 두 가지를 구하는 것으로 문제를 환원할 수 있다. 

> EndTime : 종료 시 측정한 Unix Time

> StartTime : 시작 시 측정한 Unix Time

## 2. 최소한의 통신 

~(사실 [1.경과시간](#1.경과시간)) 단에서 멈추어도 되지만.. 기능 명세에도 적혀 있고 기왕 통신 리소스를 적게 쓰면 좋으니 ))~

이전 항목에서 멈추게 되면 매번 유저가 보상 과정을 확인할 때 마다, 현재시간을 서버로 부터 가져와서 경과시간을 산출 해야한다. 

그런 비효율적인 상황을 막기 위해서 , 게임 구동 중 단 한번이라도 서버 시간을 받아 오는데 성공했다면, 그리고 그것이 믿을만 하다면 

앱이 퍼즈되거나 종료 후 재시작 되지 않는 한은 , 더 이상 서버 통신을 요청하지 않고 클라이언트 단에서 처리하면 좋을 것이다. 

방법은 UnityEngine.Time.unscaledTime 활용하면 충분히 가능하다. 

빠른 해결책으로는 [unbiasedtime for unity3D](https://github.com/Lordinarius/unbiasedtime)) 이런 플러그인도 있더라. 

구글 ntp 서버로 시간을 받아오고 , 지속적으로 UnityEngine.Time.unscaledTime 를 이용해 시간을 맞춰 나가는 식인 것 같은데

써보니 ntp 서버를 받아오는 것과 로컬 부분이 좀 묘하다. 적당히 개조해서 쓰면 될 것 같다. MIT 라이센스니까.

생각해둔 알고리즘은 다음과 같다. 

<div class="mermaid">
graph LR;
    start[게임 시작]
    wait[대기 & 다른 기능 작동]
    endGame[게임 종료]
    checkNetwork{최초 인터넷 연결 확인}
    checkNetwork_2{기존에 인터넷 연결 되었던 유저인가?}
    beginWatch[기준시 저장 & 로컬 타이머 작동]
    checkWatch[현재시 산출 & 유저 요청 시간으로 저장]
    userRequest((유저 보상 요청))
    userReward((유저 보상 확인))
    popupRequestInternet[인터넷 접속 요청 UI 팝업]
    start --> checkNetwork 
    checkNetwork -- Yes --> beginWatch 
    checkNetwork -- No --> wait 
    wait --> userRequest 
    userRequest --> checkNetwork_2 
    checkNetwork_2 -- Yes --> checkWatch 
    checkWatch --> wait 
    checkNetwork_2 -- No --> popupRequestInternet 
    popupRequestInternet --> checkNetwork_2
    wait --> userReward 
    userReward -->checkNetwork_2
    wait --> endGame
</div>
