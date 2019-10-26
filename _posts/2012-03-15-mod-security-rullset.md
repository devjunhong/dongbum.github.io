---
title: mod_security 설치와 룰셋
date: 2012-03-15T15:19:44+09:00
categories:
  - Linux
tags:
  - mod_security
  - 웹방화벽
---
각종 Injection 공격과 웹서버를 향한 공격을 방어하기 위한 웹방화벽 프로그램들이 많이 나와있는데 내 경우에는 공개소프트웨어인 mod_security를 쓰고 있다.

사실 mod_security 자체는 설치하기 어려운 것은 아니고 설치방법에 대해서는 문서들도 많이 있는데 문제는 방어규칙을 설정해주는 룰셋파일을 찾기 어렵다는 것.

더군다나 룰셋이란게 서버마다, 관리자마다 다 다르게 설정해서 쓰고 있을 것이므로 내 경우에는 가장 보편적인 룰셋파일을 찾아서 쓰기로 했다. kisa에서 배포하는 룰셋을 찾아갔다. 그런데 대부분의 mod_security 설치/설정 문서에 포함되어 있는 kisa 룰셋 파일 다운로드 링크는 다 깨져있었다. 윽...

며칠 찾다가 kisa 관리자에게 어제 메일을 보냈는데 답장은 오지 않았다.

오늘 다시 찾아보다가 발견.

<http://toolbox.krcert.or.kr/MMBF/MMBFBBS_S.aspx?MENU_CODE=69&BOARD_ID=17>

위 링크를 찾아가면 다운로드 받을 수 있다.

비록 자료는 2009년 3월 자료이긴하나 보편적 환경에서는 괜찮게 쓰일 수 있을 것 같다.