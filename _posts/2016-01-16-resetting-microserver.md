---
title: MicroServer를 재설정
date: 2016-01-16T16:05:19+09:00
categories:
  - MicroServer
tags:
  - CentOS
  - linux
  - rtorrent
  - Transmission
  - 리눅스
  - 토렌트
---
집에 설치한 서버에 CentOS 7을 설치해서 썼었지만 다시 6 버전으로 돌아가기로 결정.

7 버전에 적응하려 했지만 6을 쓰던 습관으로 계속 쓰기에는 너무나 불편한게 많아 가장 익숙한 시스템으로 이동했다.

Transmission 데몬을 계속 쓰다가 rtorrent를 쓰려고 했는데 속도는 rtorrent가 훨씬 좋았지만 문제점이 많았다.

  1. 다운로드 완료 디렉토리와 다운로드 진행중 디렉토리를 개별로 설정할 수 없어서 하드디스크를 나누어서 사용할 수 없다는 점
  2. 파일질라에서 sftp로 접속해서 다운로드된 파일을 이동하려 하니 오류 나면서 이동이 안됨. SSH로 접속해서 이동시켜야함.
  3. Transmission GUI 툴 같은 편리한 툴이 없어서 ruTorrent를 이용해 웹브라우저로 접속해서 토렌트 파일을 업로드 해야한다는 점.

사실상 속도가 빠르다는 점 하나 빼고는 모든 면이 Transmission에 비해 안 좋기 때문에 그만 사용하기로 결정.

주말에 시간을 내어 다시 CentOS 6.7 버전으로 설치하고 디스크 마운트하고 각종 프로그램을 재설치 했다.
