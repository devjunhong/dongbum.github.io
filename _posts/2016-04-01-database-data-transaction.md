---
title: 서로 다른 DB 머신에서 데이터 트랜잭션 처리
date: 2016-04-01T22:29:42+09:00
categories:
  - Database/SQL
  - Note of the wrong answers
tags:
  - Database
  - SQL
  - 데이터베이스
  - 트랜잭션
  - 트리거
---
오랫만에 이곳에 글을 쓴다. 신입사원으로 지원시 열심히 썼었던 잊고 있던 오답노트를 다시 정리해본다. 경력이 3년이 넘었는데 아직도 이러한 문제조차 모르는 내 자신을 반성하며 다시 정리한다.

판교의 N 게임사에서 받은 질문.

> Q. DB 머신이 물리적으로 서로 다른 머신일 때 어떠한 DB 작업시 트랜잭션 처리를 어떻게 하는가?
>
> A. 하나의 단일 머신에서 처리해서 그러한 것에 신경 쓰지 못했다.

역시 정답을 말하지 못했다. 사실 이러한 처리가 필요하다는 것을 꽤 오래전에 인지했지만 실제로 해본적이 없어서 제대로 대답을 할 수 없었다. 실제로 3년간 했던 프로젝트들 전부 단일 DB 머신에서 처리했던게 사실이고.

다시 찾아본 정답은 다음과 같다.

출처 : 네이버지식인 (<http://kin.naver.com/qna/detail.nhn?d1id=1&dirId=10205&docId=68228257>)

MSSQL을 기준으로하며, 서로 링크드 서버로 연결되어 있어야 한다는 전제가 붙는다.

변경할 테이블에 트리거를 생성한다.

```sql
CREATE TRIGGER dbo.트리거명 ON dbo.A서버테이블명
FOR UPDATE
AS

DECLARE @I_NO char(4) --변경 전
DECLARE @D_NO char(4) --변경 후

Select  @D_NO =NO --변경 전 값
From  DELETED

Select  @I_NO =NO --변경 후 값
From  INSERTED

--분산트랜잭션 처리(링크드 서버 UPDATE시 에러 없으면 에러 나는 경우가 존재합니다.)
SET XACT_ABORT ON

UPDATE [220.123.123.120].B서버DB명.DBO.B서버테이블명
SET NO = @I_NO
WHERE ID = @D_NO

SET XACT_ABORT OFF
```

결론적으로 문제의 해답은 **변경할 테이블에 트리거 처리를 한다.** 이고 그것을 위해 **XACT_ABORT_ON**과 **XACT_ABORT_OFF** 두개의 명령어를 사용해야한다는 것이다.

그렇다면 방금 처음 본 XACT_ABORT_ON/OFF가 도대체 뭔지 찾아보았다. 이에 대한 내용을 가장 잘 설명해준 글이 있었다.

<http://fbshot.blog.me/80162695844>

가장 중요한 차이점은 다음과 같다.

만약 프로시져 안에 INSERT 쿼리가 두개가 있는 상태에서 두번째 INSERT 쿼리에서 오류가 난다면,

  * `XACT_ABORT_ON`을 해놓으면 트랜잭션 안에 묶인 여러 쿼리 중 하나만 실패해도 전부다 실패처리하고 롤백한다.
  * `XACT_ABORT_OFF`일 때에는 첫번째 INSERT는 적용되고 두번째 INSERT 쿼리만 롤백한다.

이것을 이용해 배치쿼리에서 트랜잭션 처리에 대한 문제를 해결할 수 있다.

면접하면서 배치쿼리를 사용해봤냐는 질문도 받았는데 이 내용도 관련되어 있던 내용이었다.

배치쿼리와 트랜잭션에 대해 앞으로 잘 알아두어야 할 것 같다.

**2016년 4월 4일 추가.**

회사 동료 광연씨와 얘기해본 결과, 메시지큐나 웹서버 등의 미들웨어를 두고 여기에서 트랜잭션 처리를 하는게 더 좋지 않느냐는 결론에 이르렀다. 링크드서버로 연결된 DB를 이용해 트랜잭션을 이용하는 것은 적절하지 않은 해답일 것 같다. 메시지큐나 다른 미들웨어를 이용하여 이 문제를 해결하는 방법을 찾아보고 있다.