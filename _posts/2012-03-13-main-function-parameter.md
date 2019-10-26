---
title: main() 함수에 파라미터를 입력하여 명령어 제작
date: 2012-03-13T10:27:43+09:00
categories:
  - C/C++/MFC
---
다음과 같은 코드가 있을 때

```cpp
void main(int argc, char *argv[])
{
}
```

argc는 명령어와 파라미터를 총합한 개수이다. 즉 대부분의 DOS와 Unix/Linux 명령어들은 최소1을 가지며 파라미터가 2개인 경우에는 3을 가진다.

argv는 배열의 포인터로 명령어를 포함하여 파라미터를 포함하여 입력된 각 단어의 문자열의 주소를 포인터로 가지는 배열이다.

이 경우

```cpp
fopen(argv[i])
```

의 형태로 파일을 열 수 있다.