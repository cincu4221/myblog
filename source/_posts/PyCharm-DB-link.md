---
title: PyCharm, PostgresSQL 연동
date: 2022-01-11 13:14:23  
categories:   
- DB

tags:
- PyCharm
- DB
- Database
- PostgresSQL
- Link
---


이번 포스팅에서는 PyCharm에 DB를 연동하는 방법을 포스팅 한다.

포스팅에서 필자는 PostgreSQL을 사용한다.

포스팅의 대략적인 길이를 보면 알겠지만 매우 간단하다.


![](/images/PyCharm-DB-Link/Untitled.png)

먼저 본인이 연결하고싶은 위치에 파이참을 실행시켜준다.

![](/images/PyCharm-DB-Link/Untitled%201.png)

이후 좌측상단의 File > Settings > Plugins 으로 들어가면 위와 같은 화면이  열린다.

파이참에 여러가지 플러그인을 설치할 수 있는 창이다.

![](/images/PyCharm-DB-Link/Untitled%202.png)

이후 data를 검색하고 Database Navigator를 INSTALL 해준다. (필자의 경우 미리 돼 있음)

![](/images/PyCharm-DB-Link/Untitled%203.png)

그런 다음 View > Tool Windows > DB Browser를 실행시킨다.

DB Browser가 보이지 않을경우 파이참을 종료후 다시 실행해보면 된다.

![](/images/PyCharm-DB-Link/Untitled%204.png)

Database Navigator를 해당 폴더에서 처음 실행했다면 DB Browser에 Nothing to show라는 문구가 뜰 것이다.

+ 버튼을 누르고 자신이 사용할 DB를 선택해준다.

필자는 PostgreSQL를 설치했고 사용할 것이니깐 PostgreSQL를 클릭

![](/images/PyCharm-DB-Link/Untitled%205.png)

PostgresSQL에서 따로 설정을 만지거나 하지않았다면

User = postgres  
Password = DB생성시 자신이 입력한 비밀번호(또는 기본값 5432)

이외에 항목을 무언가 바꾸었다면 어떤 항목에 손대야 하는지는 독자 자신이 더 잘 알것이다.

![](/images/PyCharm-DB-Link/Untitled%206.png)

우측 하단에 TEST CONNECTION을 누르고 위와 같은 화면이 뜬다면 Apply 후 OK

여기까지 잘 따라왔다면 이제 끝났다.

![](/images/PyCharm-DB-Link/Untitled%207.png)

DB Browser에서 DB가 잘 불러와진 것을 확인하면 된다.

만약 SQL파일을 갖고있다면 이젠 PyCharm에서 전체실행, 라인별로 실행도 가능하다.