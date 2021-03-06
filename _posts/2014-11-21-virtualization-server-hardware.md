---
title: '가상화를 위한 준비 #1 - 서버 하드웨어'
date: 2014-11-21T11:32:13+09:00
categories:
  - Virtualization
tags:
  - ESXi
  - Hardware
  - Server
  - Virtualization
  - 가상화
  - 서버
  - 하드웨어
---
가상화를 위한 서버 하드웨어와 네트워크를 준비할 때의 참고사항을 정리해본다.

일단 서버 하드웨어를 준비해야했다.

보유하고 있는 서버는 HP DL120G7 기본형 모델이었다. Intel Xeon E3-1220 프로세서와 4GB ECC 메모리, 250GB 하드디스크를 장착한 1U 사이즈 서버이다.

ESXi를 설치해서 게스트 운영체제들을 운영할 때 중요한 것은 CPU보다는 메모리와 디스크이다.

#### 메모리

![](/assets/images/server-memory.png)

메모리는 게스트 운영체제마다 개별적으로 쓰는 부분이라 내가 설치할 게스트 운영체제들이 모두 쓸 메모리의 크기에 예비용 메모리량과 시스템이 사용하는 메모리량을 고려해야한다. ESXi도 일종의 운영체제이므로 메모리를 사용하게 된다. ESXi를 실제 운영시에는 2.5GB 정도 사용하고 있으나 약 4GB 정도는 ESXi가 쓴다고 예측하면 좋을 것 같다. 참고로 ESXi는 4GB 미만의 메모리에서는 설치 자체가 되지 않는다. 4GB의 메모리를 가지고 있다 하더래도 비디오메모리 등으로 공유메모리가 나가게 되어 실제 가용메모리가 4GB가 되지 않으면 설치가 되지 않는다. 결국 메모리는 8GB ECC 메모리를 4개 장착해서 32GB로 설치했다.

#### 하드디스크

![](/assets/images/western-digital-blue-wd10ezex-hard-drive.png)

디스크는 사실 요새 가격이 너무 떨어졌기 때문에 용량을 증설하는데에는 어려움이 없으나 가상화를 하게되면 디스크 속도가 저하되므로 이에 대해 고민해봐야한다. 많은 커뮤니티 사이트들과 카페를 돌아다녔을 때, SSD로 하면 쾌적한 성능이 나온다고 되어있으나 여유롭게 운영체제를 이것저것 설치해보기에는 SSD는 비용이 너무 많이 든다는 문제가 있었다. 결론적으로 하드디스크는 기존에 설치되어있던 하드디스크를 모두 제거하고 Western Digital의 7200RPM 1TB 하드디스크를 두개 구입하여 넣었다. 차후에도 디스크를 더 추가할 계획을 가지고 있다.

실제 운영 상황에서 CPU는 아직까지 크게 모자라지 않았으나 예측대로 메모리는 많이 소모되었다. 디스크는 스왑메모리 때문에 그런지 생각보다 공간이 많이 소모되었다. 디스크를 처음부터 크게 장착하는 것이 좋을 것 같다.

이정도 하드웨어를 준비해서 실제 운영을 시작했는데 사실 자원은 굉장히 여유로웠다. 대부분의 경우에 CPU는 모든 서버들의 사용량 총합이 500MHz가 채 되지 않았다. 이걸 본다면 막강한 CPU를 장착하고도 효율적으로 쓰지 못하는 서버들이 얼마나 많은지 알만하다.
