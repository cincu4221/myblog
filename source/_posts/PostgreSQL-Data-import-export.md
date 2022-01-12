---
title: PostgreSQL Data 불러오기, 내보내기  
date: 2022-01-11 13:42:22  
categories:   
- PostgreSQL  

tags:
- SQL
- DB
- PostgreSQL
- Data
---

DB를 사용하다보면 데이터를 불러와야할 일도, csv파일 등으로 내보내야 할 일도 있다.

처음 사용하는 사용자에겐 이 과정이 상당히 복잡하기 때문에 배운것을 기록 해 둘겸 남에게 쓰임새 있게 쓰이길 바라며 포스팅 시작.

## 사전 준비

- DB 로그인이 가능한 pgAdmin(PostgreSQL 관리 프로그램)
- 사용 가능한 .csv, .dump 파일

# Data import

![](/images/PostgreSQL-Data-import-export/Untitled.png)

좌상단의 File > Preferences > Paths > Binary paths 에서

※  **EDB Advanced Server Binary Path**가 아닌 **PostgreSQL Binary Path** 에 위 사진처럼 자신의 `이하경로/PostgreSQL/버전/bin` 을 입력해준다

잘 입력했다면 Set as default를 누르고 Save.

![](/images/PostgreSQL-Data-import-export/Untitled%201.png)

이젠 적용할 테이블에 우클릭을 한 후, Import/Export... 을 클릭해준다.

![](/images/PostgreSQL-Data-import-export/Untitled%202.png)

Import/Export 는 Import로

Filename은 테이블에 적용하고 싶은 파일을 찾아주고

Header를 Yes로

Delimiter는 파일마다 다를수 있는데 필자의 경우 파일을 메모장으로 열어봤을때 구분이 쉼표로 되어있기때문에 ,로 골라주었다.

OK로 적용해주고

![](/images/PostgreSQL-Data-import-export/Untitled%203.png)

테이블 리프레쉬~

![](/images/PostgreSQL-Data-import-export/Untitled%204.png)

이후 Query Tool을 열어 테이블을 조회해주면 깔끔히 적용된 모습이 출력된다.

# Data export

PostgreSQL의 데이터 export 방법에는 두가지가 있다.

![](/images/PostgreSQL-Data-import-export/Untitled%205.png)

첫째는 pgAdmin 을 통해 위 사진에 있는 Save results to file 버튼을 클릭하여 csv로 다운로드 받는법.

이는 직관적이고 쉽지만 항상 pgAdmin을 통해 다운받을수는 없으니 다른 방법도 알아보려 한다.

둘째는 CMD 를 통해 csv를 다운받는 법이다.

그러기 위해서는 미리 원하는 형식의 sql파일을 만들어 놓아야 한다.

가령 cities 테이블 전체를 내보내려면

```sql
SELECT * FROM cities;
```

가 작성된 sql 파일을 미리 만들어 놓아야 한다.

이번 포스팅에서는 이 파일 이름이 cities.sql이라 가정하고 포스팅을 작성한다.

이후 CMD에서 할 일은 다음과 같다.

먼저 파일이 있는 곳으로 이동해야 한다

```powershell
cd [cities.sql이 있는 경로]
```

이제 다음의 명령을 입력해 cities.sql의 출력값을 그대로 csv로 출력하면 된다

```powershell
psql -U postgres -d postgres -f cities.sql -o cities.csv -F ',' -A -t

-- 명령어의 뜻은 다음과 같다.
-- -U = 데이터베이스 사용자 이름
-- -d = 연결할 데이터 베이스 이름
-- -f = 파일 내부의 지정한 명령을 실행후 끝냄
-- -o = 쿼리 결과를 파일(또는 |파이프)로 보냄
-- -F = unaligned 출력용 필드 구분자 설정(기본값: "|")
-- -A = 정렬되지 않은 표 형태의 출력 모드
-- -t = 행만 인쇄
```

어후 복잡하다. 

그래도 `psql --help`를 입력하면 모든 명령어가 출력되니 참고하며 쓰면 된다.

위의 명령어를 입력하면 DB의 암호 입력창이 나오는데 DB를 만들때 입력했던 암호를 입력하면 csv생성이 완료된다.

## dump파일 업로드
psql -U postgres -d postgres -f function_example.dump