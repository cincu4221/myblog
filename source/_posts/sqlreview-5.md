---
title: SQL리뷰 수업 코드정리-5  
date: 2022-01-18 13:22:44  
categories:   
- SQL 

tags:
- SQL
- query
- stub
---

## 5일차 코드

---

### Discus_Gold_Medal

```sql
-- 성별, 연도 (2004, 2008, 2012), 현재 국가 (as Champion), 이전 국가
-- 조건 : Event명 'Javelin Throw', Medal = Gold
WITH Discus_Gold_Medal AS ( -- 아래 서브쿼리의 이름
	SELECT
		gender -- 성별, 연도, 종목, 국가(as 챔피언)
		, year
		, event
		, country AS champion
	FROM summer_medals -- 조회 테이블
	WHERE
		Year IN (2000, 2004, 2008, 2012) -- year컬럼이 2000, 2004, 2008, 2012 중에 하나이며
		AND Medal = 'Gold' -- medal컬럼이 Gold이며
		AND Event = ('Javelin Throw')) -- event컬럼이 Javelin Throw 인것
		
SELECT
	gender -- 성별, 연도, 종목, 현재 1위국가,
	, year
	, event
	, champion,
	LAG(Champion) OVER -- LAG(컬럼, 숫자(기본값1)) = 괄호안의 컬럼의 이전값(숫자만큼)을 건너뛰고 가져와 컬럼을 새로 만듦,
	(PARTITION BY gender ORDER BY Event ASC, Year ASC) AS -- 파티션을 gender로 분류, event와 year의 오름차순 정렬
	Last_Champion -- as Last_Champion
FROM Discus_Gold_Medal -- 위에서 생성한 Discus_Gold_Medal 테이블에서 조회
	ORDER BY gender asc, year ASC; -- gender, year의 오름차순 정렬
```

![위 쿼리의 출력](/images/sqlreview-5/Untitled.png)

서브쿼리가 정렬되어 출력되고, last_champion이 바로 전 대회의 우승국을 출력하는것을 볼 수 있다. 

### Athletics_Gold

```sql
-- 경기종목을 2개로 추가 ('100M', '10000M')

WITH Athletics_Gold AS ( -- 이하 서브쿼리의 이름
	SELECT
		gender -- 성별, 연도, 종목, 국가(as champion) 조회
		, year
		, event
		, country AS champion
	FROM summer_medals -- 조회 테이블
	WHERE
		Year IN (2000, 2004, 2008, 2012) -- year컬럼이 2000, 2004, 2008, 2012 중에 하나이며
		AND Medal = 'Gold' -- medal컬럼은 Gold
		AND Event IN ('100M', '10000M')) -- 100M 또는 10000M 종목인것
		
SELECT
	gender -- 성별, 연도, 종목, 현재 1위국가
	, year
	, event
	, champion,
	LAG(Champion) OVER
	(PARTITION BY gender, event ORDER BY Year ASC) AS -- 파티션을 gender와 event로 분류하고 year의 오름차순으로 정렬
	Last_Champion -- as Last_Champion
FROM Athletics_Gold -- 위 쿼리에서 생성한 Athletics_Gold 테이블에서 조회
	ORDER BY gender asc, event ASC, year ASC; -- gender, event, year의 순서대로 오름차순 정렬
```

![위 쿼리의 출력](/images/sqlreview-5/Untitled%201.png)

### DiscusThrow_Gold

```sql
-- year, athlete, future_champion(3회 이후 챔피언)
-- 조건 : Medal =Gold / event = discus Throw / gender women / year >= 1992
-- lead(컬럼명, 3) over()
WITH DiscusThrow_Gold AS ( -- 이하 서브쿼리의 이름
	select
		year -- 연도, 선수 조회
		, athlete
	from summer_medals -- 조회 테이블
	where 
		medal = 'Gold' -- 조건들 : medal컬럼이 Gold이며,
		and event = 'Discus Throw' -- event컬럼이 Discus Throw,
		and gender = 'Women' -- gender컬럼이 Women,
		and year >= 1992 -- year컬럼이 1992 년 이후인것
)

select
	year -- 연도, 선수, future_champion
	, athlete
	, lead(athlete, 3) over -- lead(컬럼, 숫자(기본값1)) = 괄호안의 컬럼의 이후값(숫자만큼)을 건너뛰고 가져와 컬럼을 새로 만듦
	() as future_champion -- as future_champion
from DiscusThrow_Gold; -- DiscusThrow_Gold 테이블에서 조회
```

![위 쿼리의 출력](/images/sqlreview-5/Untitled%202.png)

이전까지 쿼리에서 사용된 LAG함수와 LEAD함수는 다음 절에서 설명한다.

## LAG() 함수와 LEAD() 함수

---

### LAG() 함수

![LAG 함수의 사용 예](/images/sqlreview-5/Untitled%203.png)

LAG함수는 보통 `LAG(column, n(기본값1))`의 형태인데 이는 현재 행 앞의 행에 있는 열의 값을 반환한다.

그렇기 때문에 위 사진에서 last_champion의 첫번째 결과는 null이 된다(앞의 결과가 없기때문)

이후 부터는 champion컬럼의 결과가 차례로 출력된다.

참고로 5번 열에서의 null은 gender를 partition by로 나누었고 현재 행의 앞의 열을 분리시킨상태이기 때문에 null값이 조회된다.

---

### LEAD() 함수

![LEAD 함수의 사용 예](/images/sqlreview-5/Untitled%204.png)

기본적인형태는 `LEAD(column, n(기본값1))`의 형태이며,

LEAD 함수는 LAG 함수와는 반대로 현재 행 뒤의 행에 있는 열의 값을 반환한다.

사진에서 사용한 코드는 `LEAD(athlete,3)` 이므로 3칸 뒤의 열의 값을 반환한다.

이후 athlete컬럼의 결과가 차례로 출력되며 3번열 이후의 값은 존재하지 않기때문에 null이 반환된다. 