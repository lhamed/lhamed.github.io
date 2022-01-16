---
layout: post
title: Docker 를 이용한 Jenkins 의 빌드 환경 관리
description: 
modified: 2022-1-16
tags: [docker, jenkins , ci-cd, ci, cd]
image:
  credit: lhaemd
  creditlink: lhamed.github.io
---

# 직면한 문제 상황

### 문제는 예견된 위험에서 온다. 

최근 재택 근무를 자주 진행했는데, 우연히 회사의 ci/cd 툴로 사용하고 있던 Mac 빌 드머신 이상이 생겼습니다. 

원래 의도했던 날에 빌드를 못했을 뿐 아니라, 자칫 빌드 머신의 Jenkins 설정을 처음부터 다시 진행해야할 지도 모른다는 위험성을 인지했습니다. 

### 다른 대안에 대한 판단

환경 관리에 대해서 예전에 Jenkins-Configuration-As-Code 등의 플러그인을 사용해보기는 했지만, 다음의 이유들로 채택을 기각했습니다. 

1. 공식 문서와 해당 플러그인 대시보드에서, Export 와 Import 사이의 "완벽한 기능" 보장을 하지 않음.
2. Jenkins 플러그인 하나에 우리의 주력 서비스의 빌드를 기대는 것은 위험함. 

### 결론은 Docker ! 

따라서, 전부터 눈독들였던 Docker 를 이용한 Jenkins 의 환경관리를 진행하기로 했습니다. 

이에, 혹시 도움이 될만한 자료를 찾고 계신 분들에게 도움이 될까 해서 블로깅합니다. 


# 개념과 이론 

### 밑밥 

적정 기술이라는 말이 있습니다. 이는 첨단 기술과 달리, 실제 서비스나 산업에서 필요하거나 적합한 기술 수준이 있다는 개념입니다. 

Docker에 대해서 깊은 이해를 마치고, 실제 프로젝트에 들어가면 너무 좋겠지만 우리(인류)는 늘 자원과 시간이 부족합니다. 

필요한 개념만 습득하고 곧바로 구축에 들어갔습니다. 

### Docker 란?

docker.com 에 나와있는 Docker 측의 표현은 다음과 같습니다. 

> Docker makes development efficient and predictable

> 개발을 효율적으로 만들고, 예측 가능하게 만든다. 

개발을 진행하다보면, 방에 먼지가 들어앉듯 복잡성이 커집니다. 결국 이 복잡성의 대부분은 의존성 떄문입니다. 

일부 환경변수에 의존하거나, 운영체제의 설정, 플러그인의 버전 등 모든 의존성을 docker container 에 담아 복잡성을 통제할 수 있다면 마침내 Predictable 한 개발을 즐길 수 있겠지요. 

### Docker의 다음 개념들은 알아야 되더라구요. 

docker container
  - docker image 를 기반으로 container를 run 시킬 수 있습니다. 
  - 단, container 내부에서 만든 파일 등의 데이터는 docker volume 에 저장됩니다. 

docker image 
  - docker container 를 image 로 build 할 수 있습니다. 
  - docker hub 라는 저장소에서 관리되는 것을 pull 해서 사용할 수도 있습니다. 

docker volume 
  - docker container 내부의 데이터를 따로 저장합니다. 
  - mount 를 이용해서 host os 의 폴더를 연결할 수 있습니다. 
  
docker-compose 
  - docker container 생성 시 설정을 yml 파일 포맷으로 저장합니다. ( CLI 대신 파일을 이용합니다. )

dockerfile
  - docker container 생성 후 설정을 go 언어 스크립트로 작성합니다. ( 저는 아직 사용하지 않았습니다. ) 

# 작업 

### 작업의 목표와 전략

Docker 로 Jenkins lts 버전 이미지로 Container 를 생성하고, 이에 mount 되는 volume 은 git 을 이용해 저장 및 관리합니다. 

기존의 빌드머신은 Jenkins 의 ssh 슬레이브로 유니티 빌드와 테스트 코드 검사만을 진행하도록 하고, 새 마스터 Jenkins 는 AWS 인스턴스로 관리하고, 따로 개발자의 노트북에서도 언제든 작동하도록 합니다. 

이를 통해, 빌드의 안정성과 생산성을 확보합니다. ( 빌드 환경 관리에 신경쓰지 않는 게임 클라이언트 개발 업무는 일종의 복지라고 확신합니다 ! ) 

### 사용했던 소스들 

docker-compose-jenkins.yml 
``` yml 
version: '3.3'
services:
  jenkins:
    image: jenkins/jenkins:latest
    restart: always
    container_name: "jenkins"
    user: root # volume 을 mount 해서 사용하면, 권한 관련 이슈가 일어나서 추가했습니다. 
    ports:
      - "8080:8080"
    volumes:
      - ${마운트 대상폴더경로를 입력하세요!}:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock 
    privileged: true  # volume 을 mount 해서 사용하면, 권한 관련 이슈가 일어나서 추가했습니다. 
```

터미널에서 위의 파일을 이용해 container 를 실행시킵니다. 
-d 옵션은 백그라운드 실행을 의미합니다. 
-f 옵션은 file 을 의미하는 듯 합니다. 

``` zsh
sudo docker compose -f docker/docker-compose-jenkins.yml up -d
```

### 관련 파일 관리

저 같은 경우는 , ${마운트 대상폴더경로를 입력하세요!} 이 폴더 내에 폴더를 따로 하나 더 파서, docker-compose-jenkins.yml 파일을 넣어두었습니다. 
git을 통해서 버전관리 하기 편하게 하기 위해서입니다. 

# 후기

처음 해보는 작업은 너무 신납니다. 특히 인프라를 통제할 수 있게 되었다는 것은! 즐거운 코드리뷰와 더 건강한 개발문화에 다가선 것이 아닐까요! 
게다가, 운영체제에 대한 제 지식의 추악하고 광활한 빈칸을 알게 되어서 좋았습니다.
읽어주셔서 감사합니다. 

# 참고한 자료들 (감사합니다!) 

https://docs.docker.com/
https://www.redhat.com/ko/topics/containers/what-is-docker

