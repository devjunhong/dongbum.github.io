---
title: Lightsail 로 서버 이전 후기
date: 2017-11-02T14:36:24+09:00
categories:
  - AWS
  - Lightsail
  - Linux
tags:
  - Amazon
  - AWS
  - Lightsail
  - nginx
  - 가상서버
  - 리눅스
  - 아마존
---
계속 사용해오던 cloudv의 가상서버에서 aws의 새로운 서비스인 lightsail로 이전했다.

굳이 웹호스팅을 쓰지 않고 가상서버로 구성해서 사용하는 것은 git 저장소도 한몫했는데 일단 혼자서 사용하다보니 뭐하러 이런걸 해야하나...라는 회의감과 그럴거면 차라리 github에서 사람들과 같이 코드를 만들고 올리고 하는게 더 낫겠다는 생각이 들었기 때문이었다. 그래서 차라리 웹데이터들은 더 저렴한 lightsail로 이전하고 git 데이터들은 github.com 으로 이전하기로 했다.

![](/assets/images/hemanth-amazon-lightsail-01.png)

lightsail은 사용해보니 그냥 흔히 알고있는 가상서버다. 우리나라에서는 이미 많이 서비스하고 있는.

그런데 가격이 생각보다 싸다. 내 경우에는 월 5달러의 제일 저렴한 리눅스 서버로 골랐다. 메모리 512MB에 20GB의 디스크다. 디스크야 어차피 git 데이터가 github로 넘어간 이상 많이 필요치 않았지만, 너무 적은 메모리와 알 수 없는 cpu 성능 때문에 고민을 했다. 고민 끝에 최대한 메모리를 적게 쓰도록 아파치를 쓰지 않고 nginx로 쓰기로 했다.

그리고 어차피 방문객이 많지도 않고 방문객이 많으면 인스턴스를 늘리면 끝이니까.

![](/assets/images/enable-nginx-debug-logging.png)

bitnami의 여러 스택이 있었는데 사용하기 편하게 wordpress 스택을 선택하려 했지만 이 경우에는 멀티사이트를 만들기에 불편할 것 같아서 그냥 nginx 스택을 선택하고 직접 설정해서 아내의 홈페이지와 내 블로그 두개를 설치했다. nginx 설정 파일이 익숙치 않아서 약간 헤매었지만 금방 적응했다. bitnami류의 패키지 시스템이 마음에 들지 않았지만 직접 써보니 생각보다 괜찮았다. 멀티앱/멀티사이트간 여러 설정 파일들이 서로 꼬이지 않게 잘 정리되어 있었다. (물론 그런 이유로 인해 뭔가 하나 고치려면 한참 경로를 타고 들어가야 한다는건 불편하다.)

여튼 그렇게 설치하고 아파치에서 nginx로 변경했는데 와우... 속도가 생각보다 괜찮았다. 내가 아파치로 혼자 가상서버를 쓰는 것보다 훨씬 빨랐다.

접속방법에서 약간의 불편함은 있지만 어차피 접속할 일도 별로 없고... 게다가 1TB의 트래픽은 트래픽 걱정할 필요는 아예 없을만큼 정말 여유로웠다.

며칠간 여러 데이터들을 이전해본 후기

  1. 생각보다 속도가 빠름.
    도쿄 리전이고 가상서버에다가 메모리도 겨우 512MB라서 느릴 것으로 예상했지만 기존 서버보다 훨씬 빠른 느낌. 아파치와 엔진엑스의 차이인지도...
  2. 시간대 재설정 필요함.
    설치하게 되면 서버 시간을 한국에 맞춰야한다. (<https://gist.github.com/dongbum/1673616e33fb331ff8e876ee62216988>으로 저장해둔다.)
  3. 설정파일 트리구조를 잘 파악해둘 것.
    엔진엑스에 익숙치 않거니와 구조가 좀 복잡하긴하다.
  4. DNS 응답 속도가 아주 빨라짐.
    BIND나 PowerDNS로 네임서버를 직접 구성해서 썼었는데 그렇게 쓰는것보다 lightsail에서 제공하는 DNS의 응답속도가 훨씬 속도가 빨랐다. 거의 100배 정도.
  5. lightsail의 DNS는 Route 53과 약간 다름.
    lightsail에서도 300만 쿼리까지는 무료로 DNS를 제공해주는데 사용하기는 너무 편하게 되어있지만 기능적인 면에서는 Route 53 보다는 떨어진다.
  6. 512MB의 메모리로도 충분함.
    가장 저렴한 512MB 메모리의 인스턴스로도 블로그와 몇가지 개인서비스를 운영하는데에는 차고 넘치는 느낌이다.
  7. 사용상 몇가지 불편함이 있음.
    bitnami 패키지의 특성인지 보안을 위해 암호 같은게 어렵게 설정되어 있어서 약간 불편함. 암호를 일일히 바꾸고 쓰기보다는 그냥 쓰기로 결정했다.

---

**2018년 5월 17일 업데이트**

얼마전 Lightsail 에도 서울 리전이 생겼다. 한국 사람들은 서울 리전 쓰면 될듯. 난 그냥 귀찮아서 계속 도쿄에 내버려두는 중.

**2018년 6월 27일 업데이트**

스냅샷을 생성하여 서울 리전으로 옮기려 했지만 스냅샷으로 인스턴스 생성은 같은 리전으로 밖에 되지 않았다. 리전간 스냅샷 전송기능이 생길 때까지 기다려야 할듯하다.

**2018년 12월 3일 업데이트**

리전간 스냅샷 복사기능이 생겨났다!!! 몰랐는데 아래 카리스턱님의 댓글로 알게되었다. 하지만 이 기능이 없어서 이미 난 서울 리전에 인스턴스를 생성해서 수동으로 모두 이전했다. 외국을 대상으로 서비스하다가 한국으로 이전하거나 혹은 그 반대일 때 아주 유용한 기능일듯.
