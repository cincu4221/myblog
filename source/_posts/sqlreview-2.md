---
title: SQL리뷰 수업 코드정리-2  
date: 2022-01-12 14:57:31  
categories:   
- SQL 

tags:
- SQL
- query
- stub
---

## 2일차 코드 (서브쿼리 기본)

---

![](/images/sqlreview-2/Untitled.png)

![](/images/sqlreview-2/Untitled%201.png)

![](/images/sqlreview-2/Untitled%202.png)

```sql
--실제 보유하고 있는 과일 데이터
select * from real_amount; -- 테이블값 있음, 위 이미지 첫번째 테이블

-- 카운터 컴퓨터에서 추정한 과일 데이터
select * from assumption_amount; -- 테이블값 있음, 두번째 테이블

-- 외상 데이터
select * from exception; -- 테이블값 없음, 세번째

-- 기본적으로 서브쿼리에서 true가 반환되어야 메인쿼리가 실행되는듯
-- exists(서브쿼리) == 서브쿼리의 결과가 한건이라도 존재할 경우 True 없으면 False 리턴
-- 카운터에는 데이터 존재 / 외상 데이터 현재 없음
select * from real_amount -- 현재 과일 데이터 출력
where exists ( -- 위의 exists 설명 참조
	select * from assumption_amount -- 컴퓨터 추정 과일데이터
);
-- 결과 : 컴퓨터에서 추정한 과일 데이터가 존재하니 exists == true 반환, 그러므로 메인쿼리가 실행됨

select * from real_amount -- 현재 과일 데이터 출력
where exists ( -- 위의 exists 설명 참조
	select * from exception -- 외상데이터
);
-- 결과 : 외상데이터 조회시 테이블값이 없기 때문에 exists == false 반환, 메인쿼리가 실행되지 않음
-- SQL의 아웃풋 창에는 select * from exception이 출력

-- IN 연산자 / NOT IN 연산자
-- IN 연산자 : 하나이상의 값이 도출이 되면 true
select * from real_amount -- 현재 과일 데이터 출력
where amount in ( -- amount(메인쿼리의 테이블에서 값을 받아오는 것으로 추정)값에 10, 20, 30 이 있을경우 true
	10, 20, 30
);
-- 결과 : real_amount 테이블의 amount 컬럼에 10과 30이 존재하기 때문에 메인쿼리가 실행되어 현재 과일데이터가 출력됨

-- ANY 연산자
select * from real_amount -- 현재 과일 데이터 출력 (3)
where 10 = any ( -- 서브쿼리의 출력에 10이 있을 경우 (2)
	select amount from assumption_amount
	-- assumption_amount 테이블의 amount 컬럼을 출력 (1)
);
-- 결과 : assumption_amount 테이블의 amount 컬럼에 10이 존재하기 때문에 real_amount 출력
```

![](/images/sqlreview-2/Untitled%203.png)

```sql
select * from populations; -- 위 테이블 이미지

-- 기본적인 집계함수
-- avg(*) NULL 값이 아닌 모든 입력 값의 평균

select avg(life_expectancy) from populations; -- 모든 life_expectancy의 평균값 출력

-- count(*) 입력한 행의 총 갯수
select count(*) from populations; -- populations 테이블의 모든 행 갯수 - 434

-- count(컬럼명) NULL 값이 아닌 해당 컬럼 행의 갯수
select count(life_expectancy) from populations; -- populations 테이블의 NULL이 있는 행을 제외한 life_expectancy 컬럼의 갯수 - 398

-- max, min, sum -- 모두NULL 값이 아닌 해당 컬럼 행만 계산
select max(life_expectancy) from populations; 

select min(life_expectancy) from populations;

select sum(life_expectancy) from populations;

-- 기대수명이 가장 높은 country code
select country_code, life_expectancy -- country_code, life_expectancy 출력 (5)
from populations -- populations 테이블의(4)
where life_expectancy = ( -- (2)와 동일한 life_expectancy값을 가진 행의  (3)
	select min(life_expectancy) -- life_expectancy컬럼의 최솟값(2)
	from populations -- populations 테이블의 (1)
);
-- 결과 : populations 테이블의 life_expectancy컬럼의 최소값과 동일한 life_expectancy를 가진 country_code, life_expectancy를 populations 테이블에서 찾아 출력

-- 삼중쿼리
-- 집계함수는 where절에서 사용 불가이기 때문에 서브쿼리 사용
select country_code -- country_code 출력 (8)
from populations -- populations테이블의 (7)
where code = ( -- (5)에서 선택된 테이블의 행중에 code 컬럼과 같은값을 가진 행 (6)
	select * -- (4)에서 선택된 테이블의 모든 컬럼 조회 (5)
	from countries -- countries 테이블 (4)
	where life_expectancy = ( -- (2)와 동일한 life_expectancy값을 가진 행 (3)
		select min(life_expectancy) -- life_expectancy컬럼의 최솟값 (2)
		from populations -- populations 테이블의 (1)
));
-- 복잡하다... 설명을 못해서 그렇기도 하지만, 차라리 SQL로 보는게 낫지 한글로 풀어설명하는게 더 복잡하다.

-- 조건 1. 2015년 전체 국가의 평균 수명 계산
-- 조건 2. 모든 데이터를 조회합니다.
-- 조건 3. 2015년 평균 기대수명의 1.15배보다 높도록 조건을 설정합니다.

-- 이번엔 거꾸로 과정 작성
select *  -- 모든 컬럼 출력 (1)
from populations -- populations 테이블의 (2)
where life_expectancy > 1.15 * ( -- 단, life_expectancy가 서브쿼리 값의 1.15배보다 큰것만 출력 (3)
	select avg(life_expectancy) -- life_expectancy의 평균값 출력(4)
	from populations -- populations 테이블의 (5)
	where year = 2015) -- year 컬럼이 2015인것들로만 평균값 출력(6)
	and year = 2015; -- (3)의 and조건 추가절, year가 2015 일것.
-- 결론 : 2015년도의 평균life_expectancy * 1.15 보다 크고, year 가 2015인 행의 모든 컬럼 출력 
-- 간단한 편..

	

select * from cities; -- name

select * from countries; -- capital

-- 메인쿼리
-- citi 테이블에서, name, country_code, urban_pop
-- urban_pop 내림차순 정렬
-- 상위 5개만 출력
-- 서브쿼리
-- city 테이블에 name과 countries capital 매칭이 되는 애들만 조회
select name, country_code, urbanarea_pop -- 각 컬럼 출력
from cities -- cities 테이블에서 조회
where name in (select capital from countries) -- name컬럼 내부에 서브쿼리의 값과 같은값이 있는 경우만
order by urbanarea_pop desc -- urbanarea_pop 컬럼 내림차순으로 정렬
limit 5; -- 상위 5개만

-- 결과물을 동일하게
-- 두개의 테이블을 JOIN
SELECT countries.name AS country, COUNT(*) AS cities_num
  FROM cities
      INNER JOIN countries
      ON countries.code = cities.country_code -- 테이블 교집합
GROUP BY country -- country의 항목으로 묶어줌
ORDER BY cities_num DESC, country -- cities_num 컬럼을 내림차순으로 정렬, country 컬럼 출력
LIMIT 9; -- 상위 9개만

-- 서브쿼리를 where --> select 절로 옮긴 결과
select 
	countries.name as country 
	, (select 
	   	count(*) 
	   	from cities 
	   	where countries.code = cities.country_code) as cities_num
from countries
order by cities_num desc, country
limit 9;
-- 안보던 형식이라 그런지 더 복잡해 보인다.
```