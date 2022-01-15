---
title: SQL리뷰 수업 간단정리-3  
date: 2022-01-13 16:18:20  
categories:   
- SQL 

tags:
- SQL
- query
- stub
---

## 3일차 코드

---

![languages 테이블](/images/sqlreview-3/Untitled-1.png)

![couintries 테이블](/images/sqlreview-3/Untitled-2.png)

```sql
-- 서브쿼리 쓰는 방식
-- where 절 서브쿼리
-- select 절 서브쿼리
-- from 절 서브쿼리

select * from languages;
select * from countries;

-- 질문 : 각 나라별 언어의 갯수 구하기
-- Table: languages
select code, count(*) as lang_num -- 국가 코드, 모든행을 카운트해 lang_num 으로 출력
from languages -- 사용한 테이블
group by code; -- 국가 코드로 묶을것
-- 결과 : 각각의 국가 코드로 묶인 lang_num 출력

-- 질문, country로 변경하고, 언어의 갯수 구하기
-- lang_num을 내림차순으로 정렬함.
-- 이 쿼리서 from절 서브쿼리 사용
select local_name, subquery.lang_num  -- countries 테이블의 local_name, (as)subquery 에서 lang_num을 각각 출력
from countries -- 테이블은 countries 와 다음의 서브쿼리
	, (select code, count(*) as lang_num -- 전 질문의 쿼리를 가져와 'subquery' 명칭을 붙임
	from languages
	group by code) as subquery
where countries.code = subquery.code -- countries.code 와 subquery.code가 매칭이 될 경우만 조회
order by lang_num desc; -- lang_num을 내림차순으로 정렬
-- 결과 : countries.local_name과 subquery.lang_num이 각각 lang_num의 내림차순으로 출력

--
select * from economies
where year = 2015;

-- 코드별 inflation_rate
-- 각 대륙별, 각 나라별 inflation_rate
-- 각 대륙에서 inflation_rate가 가장 높은, inflation_rate를 출력

SELECT name, continent, inflation_rate -- name, continet, inflation_rate 를 조회
  FROM countries -- countries 테이블
    INNER JOIN economies -- inner join = 기준테이블, 조인테이블 모두에 해당 값이 존재할 경우 메인쿼리 조회
    on countries.code = economies.code -- economies 와 countries.code = economies.code 에 겹치는 값이 있는지
  WHERE year = 2015 -- year항목이 2015이고
    and inflation_rate in ( -- inflation_rate 항목에 다음 서브쿼리의 값이 있는지
        SELECT MAX(inflation_rate) AS max_inf -- 가장 큰 inflation_rate를 조회
        FROM ( -- 다음의 서브쿼리에서
             SELECT name, continent, inflation_rate -- name, continent, inflation_rate 조회
             FROM countries -- countries 테이블
             INNER JOIN economies -- economies 와 
             on countries.code = economies.code -- countries.code = economies.code 에 겹치는 값이 있는지
             WHERE year = 2015) AS subquery -- year = 2015인 것만 조회 ) subquery로 명명
        GROUP BY continent); -- 바로 위에서 출력한 서브쿼리를 continent로 묶음
-- 결과 : countries테이블의 name, continent, inflation_rate 조회 group by 때문에 대륙별로 한 나라씩만 조회되었고 조회된 나라의 기준은 inflation_rate가 가장 높은 국가

```

![마지막 쿼리의 출력 결과](/images/sqlreview-3/Untitled-3.png)

첫번째와 두번째 쿼리는 직접 작성하지는 못해도 해석은 할 수 있었는데 마지막 쿼리는 정말이지 복잡했다.  
강의 뿐만 아니라 책도 구매해서 SQL를 더 파야 할 듯.