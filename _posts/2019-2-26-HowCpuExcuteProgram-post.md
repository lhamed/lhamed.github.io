---
layout: post
title: How_CPU_Excuete_Program
description: "Fri,2019.2.16"
modified: 2019-2-24
tags: [cs, SelfStudy , Study , Note]
image:
  path: /images/Lawn.png
  feature: abstract-3.jpg
  credit: lhaemd
  creditlink: lhamed.github.io
---

# CPU 가 프로그램을 어떻게 실행하는지

예를 들어 , 

어셈블리 언어 (Assembly Language) "INC A" 가 있다면 . ( A 를 Include 한다는 것 )

기계어 ( Machine Code ) 로는 "0011100" 으로 쓴다. 

이를 인간이 좀 더 읽기 쉽도록 16진수(Hexa-decimal)로 나타내면 "3C" 이다. 

이제 본론으로 들어가서 , INC A 라는 프로그램 명령어를 CPU 에서 실행하는 모습을 보자면 , 

먼저 메모리의 "AE00" 이라는 주소안에 "3C" 가 들어 있는 것이고 
```csharp 
//TODO 아마 작성된 프로그램을 의미하는 것 같다. 나중에 공부하고 아니면 수정하자 
```

PC( Program Counter )에서 다음에 실행될 명령어의 주소인 "AE00" 를 가지고 있고 ( 이 때문에 명령어 포인터 라고도 한단다. ) , 이를 MAR로 넘긴후에 프로그램 계수기는 1 증가한다. ( 그리고 다음 명령어를 넘기는 식이다. )

이후 MAR ( Memroy Address register ) 에서 이를 넘겨받아 역시 "AE00"이라는 주소 값을 가지고 있다면, 
```csharp 
//register는 참고로 컴퓨터 프로세서내의 자료를 보관하는 아주 빠른 기억 장소이다. 라고 위키에는 나와있다. 마찬가지로 나중에 더 깊게 찾아보자. 앞서 말한 PC 도 레지스터다. 
```

그 다음에 , 주소값은 Adrees Bus 를 통해 메모리에 전달되어 , 메모리의 해당 주소 ( 여기서는 "AE00") 에 전달되게 된다. 
또한 동시에 CU ( Controll Unit ) 에서는 두개의 low pulse 를 보내는데, 
```csharp 
//이거 아마 아두이노 할 때 배운 HIGH 와 LOW 펄스 얘기가 아닐까 싶다.   CS Line (Chip Switch) 와 R/W (Read & Write) Line 이 그것이다. 이 low pulse 들은 Address bus 를 통해 전달 받은 주소값에 저장된 데이터를 읽어 올 수 있게한다. 

//CU는 메모리와 CPU 간의 통신및 조율을 돕는다고 한다. 아마 읽거나 쓸 떼 지금 뭘하려고 하는지 보내는게 아닐까 싶다. 나중에 부연할 것 TODO  
``` 

그리도 다음에 "AE00"에 저장된 "3C" 데이터를 메모리는 명령의 시작 주소를 기억하는 BR (Buffer Register) 에 전달하고 , 실행중인 명령을 기억하는  IR (Instruction Refister)에 전달된다. 그리고 Docoder 를 거쳐서 명령을 해독하게 되고 , CU는 ALU ( Arithmetic and Logic Unit , 연산장치 )으로 하여금 , 3C의 명령을 실행해서 Register A 의 데이터 00H 를 01H 로 만든다. 

# 정리

                                                                                                        (Work)  <-  [ALU]
[PC] -(Addrees)-> [MAR] -(Addrees)-> [Address_Bus] -(Addrees)->        [------]                                       ^
                                     [CU] -(Low)-> [CS_Line]  -(Low)-> [Memory] -(Data)-> [BR] -> [IR] -> [Docder]-> [CU]
                                                   [R/W_Line] -(Low)-> [______]                                        

# 후기    
짧은 CPU의 프로그램 실행에 대한 동영상을 보았다. 내용은 전혀 쉽지 않았다 @_@. 

온갖 줄임말이 난무해서 분명 강의자가 천천히 말하는데도.. 그래서 3번 봤더니 조금 알것 도 같다. 

위는 정리하기 전 쓴 말이고, 정리하면서 내가 모른다는 걸 한층 더 알게 되었다. 

생각없이 써내리는 코드가 CPU 단에서는 개고생하고 있었구나 싶다 ㅎㅎ.. 

아마 위 동영상 강의는 아주 간단하고 피상적으로 설명한 거겠지. 

하루에 한개 정도면 충분히 나갈 수 있겠는데 생각보다 오래걸리지 싶다. @_@ 

아래는 감상. 

소프트웨어가 물리적으로 작동하게 되는 원리가 무척 신기하다. 

인간의 정신 활동을 생물 심리학적으로 처음 물리적 구조로 보았을 때의 느낌과 비슷하다. 

인간의 뇌도 비슷하게, 뉴런의 발화형태( 일시적 상태 )로 기억되는 일종의 임시메모리 작업기억이 있고 , 

뉴런의 연결 상태로 나타내는 비교적 영속적인 기억이 존재한다. 

그리고 이 둘의 통신.. 이라고 하나 컴퓨터로 보면 그런데

상호작용 하거나 서로 데이터가 넘어과는 과정을 감각 심리학 -> 생물 심리학 -> 인지심리학의 커리큘럼을 타며 들은 적이 있어서

원리가 매우 흡사다하는 느낌을 받았다. 

또한 의외로 아두이노로 회로 만졌던게 도움이 되는 것 같다. 

많이 하거나 깊이 하지는 않았지만, 처음인 만큼 충분히 재미있게 공부했다. 
