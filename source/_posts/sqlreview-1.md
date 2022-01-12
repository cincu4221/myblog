---
title: SQL리뷰 수업 간단정리-1
date: 2022-01-11 12:28:31  
categories:   
- SQL 

tags:
- SQL
- query
- stub
---


## 1일차 코드

---

```
-- 전체 테이블 조회
select * from subway;

-- 테이블 생성
create table develop_book(
	book_id integer
	, date date
	, name varchar(80)
);

-- 등록된 테이블 리스트 조회
-- CMD 창에서 \dt 실행하면 동일한 리스트 확인 가능
SELECT * FROM pg_catalog.pg_tables
WHERE schemaname != 'pg_catalog' AND
    schemaname != 'information_schema';

-- 테이블 삭제
drop table develop_book;

-- 테이블 생성
create table develop_book(
	book_id integer
	, date date
	, name varchar(80)
);

-- 데이터 자료 추가하기
insert into develop_book values(1, '2021-12-22', 'SQL 레시피');

-- 큰 따옴표 입력
insert into develop_book values(2, '2021-12-23', '"자바의 정석"');

-- 작은 따옴표 입력
insert into develop_book values(3, '2021-12-24', '''자바의 정석''');

-- Let's go 입력
insert into develop_book values(4, '2021-12-25', 'I''am book');

-- 조회 하기
select * from develop_book;

-- 테이블에 자료 여러 개 추가하기
insert into develop_book values
(5, '2021-12-30', '책1'),
(6, '2021-12-30', '책2'),
(7, '2021-12-30', '책3'),
(8, '2021-12-30', '책4');

-- 조회 하기
select * from develop_book;

-- 컬럼 선택 조회
select book_id, name from develop_book;

-- Limit 명령어
select * from develop_book limit 3;

-- OFFSET 명령어 추가
-- ~번째 인덱스부터 시작
select * from develop_book limit 5 offset 2;

-- ORDER BY
-- 오름차순
select * from develop_book
order by name asc;

select * from develop_book
order by name desc;

-- WHERE 조건문
select * from develop_book
where book_id = 5;

select * from develop_book
where book_id <> 5; -- 5 제외

-- AS 명령어
select name as 책제목 from develop_book;

-- Coalesc 함수
-- 데이터 조회 시, NULL 값을 다른 기본 값으로 치환
-- ex) NULL --> "데이터 없음"

insert into student_score(name, score)
values ('Hello', NULL), ('Hi', NULL);

-- 조회
select
	id
	, name
	, score
	, case
		when score <= 100 and score >= 90 then 'A'
		when score <= 89 and score >= 80 then 'B'
		when score <= 79 and score >= 70 then 'C'
		when coalesce (score,0) <= 69 then 'F'
		end
from student_score;

-- 결측치 처리
select
	students
	, coalesce((12/nullif(students, 0))::char, '나눌 수 없음') as column8
from division_by_zero;
```