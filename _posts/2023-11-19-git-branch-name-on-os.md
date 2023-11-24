---
layout: post
title: git branch name on windows and linux
description: 
modified: 2023-11-19
tags: [blog]
image:
  credit: lhamed
  creditlink: lhamed.github.io
---

# 깃 브랜치 네이밍 이슈 (git branch name is case-sensitive)

평소처럼 git을 사용해 업무를 진행하다가, 

편하게 git reset --hard를 하고 

sourceTree의 terminal,( MINGW32 기반) 을 사용해 커밋 및 푸시하고,

테스트 서버 (Linux)로 받으려니 build 브랜치를 pull 해오지 못했다. 

# 원인 

알고보니, build 브랜치 외에 Build 브랜치, 즉 앞의 대소문자만 다른 브랜치 네임이 

sourceTree의 터미널을 사용하는 도중에 생성되었고, 

linux의 파일 시스템은 windows, mac 과 다르게 대소문자를 구분하는 것이 문제의 원인이었다. 

왜냐하면 깃 브랜칭은 내부적으로 파일을 사용하기 떄문에, 파일네임이 브랜치므로 이런 이슈가 발생했다. 

# 해결 

linux 서버에서 build 브랜치와 Build를 같게 유지하고, 하나를 삭제했다.
( winodws 나 mac 에서는 대소문자 구분이 없기 때문에 고치기 힘들 것 같다. )