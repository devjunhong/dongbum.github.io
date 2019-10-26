---
title: 힙과 스택
date: 2012-09-26T15:43:00+09:00
categories:
  - C/C++/MFC
  - Note of the wrong answers
  - Programming
tags:
  - 면접
  - 스택
  - 프로그래밍
  - 힙
---
내가 면접 때 많이 들어봤던 질문 중의 하나였다.

> "힙과 스택에 대하여 설명해보세요."

C/C++을 공부하면서 당연히 배우는 과정 중의 하나인데 문제는 이런 내용은 C 처음 배울 때 나온 내용이라 기억의 저편으로 멀리 가버렸다는 점. 기억을 되살리기 위해 다시 정리해본다.

---

### 스택의 특징은...

  * 프로그램이 자동적으로 할당한 메모리 영역이다.
  * 자동변수와 파라미터들이 생성되고 스코프가 끝나면 사라지는 메모리 영역.
  * 함수가 실행된 뒤 원래 실행위치로 돌아오는 리턴값 역시도 스택에 저장된다.
  * 함수 안에서 선언된 변수는 모두 스택으로 들어간다.
  * 함수를 호출했을 때 현재 상태에 대한 값도 스택으로 들어간다.
  * LIFO 구조를 가진다. 먼저 들어간 자료가 가장 나중에 나오게 되며, 가장 나중에 들어간 자료가 가장 처음에 나오게 된다.
  * 윈도우 프로그램의 경우 기본 스택메모리의 크기는 1MByte이다.
  * 스택의 크기를 넘어가게 되면 Page Fault 인터럽트(즉, 스택오버플로우)가 발생하게 된다.
  * 모든 포인터 역시도 스택에 올라간다. 포인터 역시도 하나의 변수라는 것을 잊지말 것.
  * 사용할 스택의 크기는 컴파일 하는 순간 모두 정해진다. 따라서 실행 도중 메모리의 크기를 변경할 수 없다.
  * 스레드가 여러개라면 각 스레드마다 고유한 스택영역이 준비된다.
  * 하나의 메소드를 실행하기 위한 스택메모리의 묶음을 스택프레임이라고 부른다.
  * 어떤 변수를 선언했다면 변수명 자체는 스택에 변수 내용은 힙에 저장된다.

---

### 힙의 특징은...

  * 프로그래머가 스스로 할당한 메모리 영역이다.
  * 힙은 프로그램이 동적으로 할당받아 사용되는 메모리 영역. C에서의 malloc을 통해 생성하고 free를 통해 해제하며 C++에서는 new를 통해 생성하고 delete를 통해 메모리를 해제한다.
  * 힙 메모리가 부족하게 되면 메모리 이상현상으로 프로그램은 종료되게 된다.
  * 사용할 힙의 크기는 프로그램 실행 중 정해진다.
  * 동적 메모리할당은 프로그램 사용자들이 얼마나 데이터를 입력할지 예측할 수 없는 경우에 사용한다.
  * 여러 스레드가 있는 경우 힙 영역은 각 스레드가 공통으로 사용할 수도 있다.

---

이외에도 데이터영역과 텍스트영역(코드영역)이 있다.

---

### 데이터영역의 특징은...

  * 프로그램이 실행되고 난 후 종료될 때 까지 지워지지 않을 메모리 공간이다.
  * 따라서, 전역변수, Static 변수 등이 저장된다.
  * 프로그램당 한개의 영역이 할당된다.

---

### 텍스트영역(코드영역)의 특징은...

  * 프로그램의 실행코드를 저장한다. 프로그래머가 만든 코드, 함수는 모두 여기에 저장된다.
  * 역시 프로그램당 한개의 영역이 할당된다.

---

위의 내용들을 찾을 수 있었다. 다시금 찾아보니 생각보다 내용도 많고 차이점도 여러가지인 것 같다. 앞으로 더 찾아보며 여기에 추가해야겠다.

#### 참고자료

  * http://blog.naver.com/brosvaby?Redirect=Log&logNo=165225008
  * http://panic.kldp.org/node/199
  * http://blog.naver.com/ysjin1212?Redirect=Log&logNo=110128934379
  * http://blog.naver.com/0bloodwind0?Redirect=Log&logNo=20127908176
  * http://blog.naver.com/zelet7?Redirect=Log&logNo=140015294688