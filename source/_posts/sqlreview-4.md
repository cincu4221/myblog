---
title: SQL리뷰 수업 코드정리-4  
date: 2022-01-17 13:07:20  
categories:   
- SQL 

tags:
- SQL
- query
- stub
---
## 4일차 코드

---

![summer_medals 테이블](/images/sqlreview-4/Untitled.png)

```sql
select * from summer_medals;

-- row_number()
-- 각 행에 숫자를 1, 2, 3, ..., N 형태로 추가한다.
-- 오름차순으로 기준을 진행한다.
-- 기본적 row_num만 추가
select
	row_number() over() as row_num
	, *
from summer_medals;

-- 올림픽 연도를 오름차순 순번대로 작성을 한다.
-- 연도 중복값 제거
-- 서브쿼리 : select distinct year from summer_medals order by year asc;
select
	row_number() over() as row_num -- 각 행에 오름차순으로 숫자 추가 as row_num, year행 출력
	, year
from
	(select distinct year from summer_medals order by year asc) as years -- 중복값을 제거한 year 컬럼을 오름차순으로 출력 as years
order by year asc; -- select절의 컬럼들을 year컬럼의 오름차순으로 정렬

select * from summer_medals;

-- 운동선수 메달 갯수 쿼리 작성
with athlete_medals as (
	select
		athlete -- athlete, 전체 컬럼을 count하고 athlete로 묶음(group by절) as medal_counts
		, count(*) medal_counts
	from summer_medals
	group by athlete
)
select 
	athlete -- athlete, medal_counts, medal_counts의 내림차순으로 숫자를 붙인 row_num 출력
	, medal_counts
	, row_number() over(order by medal_counts desc) as row_num
from athlete_medals
order by medal_counts desc -- select절의 컬럼들을 medal_counts의 내림차순으로 정렬
limit 10; -- 상위 10개만 출력

-- 남자 69 KG 역도 경기에서 금메달 리스트 추출.
-- Discipline = 'Weightlifting'
-- Event 69KG,
-- Gender
-- Medal
select * from summer_medals;
select distinct event, discipline, athlete, gender  from summer_medals where event = '200M' and gender = 'Women' and medal = 'gold';

select 
	year -- 연도, 국가 as champion 출력
	, country as champion
from 
	summer_medals
where 
	discipline = 'Weightlifting' and -- 종목 = 역도,
	event = '69KG' and -- 세부종목 = 69KG,
	gender = 'Men' and -- 성별 = 남자,
	medal = 'Gold'; -- 금메달만, 상기 4개 조건 모두 만족하는결과만 출력

-- LAG

with weightligting_69_men_gold as (
	select 
		year
		, country as champion
	from 
		summer_medals
	where 
		discipline = 'Weightlifting' and
		event = '69KG' and
		gender = 'Men' and
		medal = 'Gold'
)

select
	year
	, champion
	, LAG(champion) over(order by year asc) as last_champion
from weightligting_69_men_gold
order by year asc;

-- Athletics, 200미터, 여자, 금메달 목록 가져오기
-- 나라 대신 선수이름 출력 year, 현재 챔피언 이름, 이전 챔피언 이름

with Athletics_200_Women_Gold as (
	select
		year
		, athlete as champion
	from
		summer_medals
	where
		discipline = 'Athletics' and
		event = '200M' and
		gender = 'Women' and
		medal = 'Gold'
)

select
	year
	, champion
	, lag(champion) over(order by year asc) as last_champion
from Athletics_200_Women_Gold
order by year asc;

-- partition by 함수
-- partition by 미적용
WITH Discus_Gold_Medal AS (
	SELECT 
		Year, Event, Country AS Champion
	FROM summer_medals
	WHERE 
		Year IN (2004, 2008, 2012)
		AND Gender = 'Men' AND Medal = 'Gold'
		AND Event IN ('Discus Throw', 'Triple Jump')
		AND Gender = 'Men')
		
SELECT 
	YEAR, Event, Champion, 
	LAG(Champion) OVER
	(ORDER BY Event ASC, Year ASC) AS Last_Champion
FROM Discus_Gold_Medal
	ORDER BY Event ASC, Year ASC;

-- partition by 적용
WITH Discus_Gold_Medal AS (
	SELECT 
		Year, Event, Country AS Champion
	FROM summer_medals
	WHERE 
		Year IN (2004, 2008, 2012)
		AND Gender = 'Men' AND Medal = 'Gold'
		AND Event IN ('Discus Throw', 'Triple Jump')
		AND Gender = 'Men')
		
SELECT 
	YEAR, Event, Champion, 
	LAG(Champion) OVER
	(PARTITION BY Event ORDER BY Event ASC, Year ASC) AS 
	Last_Champion
FROM Discus_Gold_Medal
	ORDER BY Event ASC, Year ASC;
```