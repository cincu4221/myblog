---
title: (ORACLE) NULL값을 치환하는 NVL, NVL2 함수
date: 2022-02-23 12:49:01  

categories:
- ORACLE

tags:  
- ORACLE
- SQL
- FUNCTION
---


SQL을 사용하다 보면 NULL을 다른 결과로 치환하여 출력하는 문제가 가끔 나온다.

오라클에서는 이를 NVL 함수로 간단히 처리 가능한데 문제가 있다면 이 쿼리를 다른 DBMS에서 사용할 때 이다.

ORACLE : NVL

MYSQL : IFNULL

MSSQL : ISNULL

세 개의 DBMS 모두 사용하는 함수가 다른데 그렇기 때문에 서로 호환이 안된다.

## NVL 함수의 사용법

```sql
-- 기본형
NVL(컬럼, NULL일 경우의 반환값)

NVL(컬럼, '') -- 컬럼의 값이 NULL일 경우 ''으로 치환함
NVL(컬럼, 0) -- 컬럼의 값이 NULL일 경우 0으로 치환함
```

### 예제

```sql
-- NAME 컬럼의 값이 NULL 일 경우 'No name'으로 치환
SELECT NVL(NAME, 'No name')
FROM ANIMAL_INS;
```

## NVL2 함수의 사용법

기본적으로 NVL함수와 비슷하나 NULL값이 아닐때도 치환을 해준다

```sql
-- 기본형
NVL2(컬럼, NULL이 아닐경우의 반환값, NULL일 경우의 반환값)

NVL2(컬럼, '학생', '교사')
NVL2(컬럼, '대중교통', '자동차')
```

### 예제

```sql
-- DATETIME 컬럼의 값이 NULL 일경우 '정규직' NULL이 아닐경우 '계약직'
SELECT NVL(DATETIME, '계약직', '정규직')
FROM EMPLOYEE;
```