---
title: "Oracle_practice1"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-05'
---

### 사전준비

- 이전 글을 참고하여 Oracle 설치한다.
- [https://www.notion.so/Oracle-setting-e380ad08eac048ebba97c7b90c69a132](https://www.notion.so/Oracle-setting-e380ad08eac048ebba97c7b90c69a132)

### 실습

- SQL Developer 에서 실행
- 테이블을 생성한다.
    - 다음 코드를 작성해보자

```sql
CREATE TABLE ex2_1 (
COLUMN1     CHAR(10)
, COLUMN2     VARCHAR2(10)
, COLUMN3     NVARCHAR2(10)
, COLUMN4     NUMBER
);
```

- 저장(ctrl + s) 후 실행(ctrl + enter)
    - 다음과 같이 테이블과 컬럼이 생성된다.

![Untitled](/images/Oracle_practice1/Untitled.png)

- 오라클 SQL과 PL/SQL을 다루는 기술 52p
- 교재를 따라 다음과 같이 작성하고 실행해 본다.
    - 스크립트 실행 = 전체 실행 = F5
    - 명령문 실행 = 일부 실행 = ctrl + enter

```sql

CREATE TABLE ex2_1 (
COLUMN1 CHAR(10)
, COLUMN2 VARCHAR2(10)
, COLUMN3 NVARCHAR2(10)
, COLUMN4 NUMBER
);

-- 데이터 추가
INSERT INTO ex2_1 (COLUMN1, COLUMN2) VALUES('abc', 'abc')

-- 데이터 확인
SELECT
COLUMN1
, LENGTH(COLUMN1) as len1
, COLUMN2
, LENGTH(COLUMN2) as len2
FROM ex2_1;

-- 새로운 테이블 생성
CREATE TABLE ex2_2(
COLUMN1 VARCHAR2(3)
, COLUMN2 VARCHAR2(3 byte)
, COLUMN3 VARCHAR2(3 char)
);

-- 데이터 추가
INSERT INTO ex2_2 VALUES('abc', 'abc', 'abc');

-- 조회
SELECT
COLUMN1
, LENGTH(COLUMN1) As len1
, COLUMN2
, LENGTH(COLUMN2) As len2
, COLUMN3
, LENGTH(COLUMN3) As len3
FROM ex2_2;

-- 한글 데이터 삽입
-- 에러 발생
INSERT INTO ex2_2 VALUES('홍길동', '홍길동', '홍길동');

- 데이터 조회
SELECT
COLUMN3
, LENGTH(COLUMN3) As len3
, LENGTHB(COLUMN3) As bytelen
FROM ex2_2;

- 숫자 데이터 삽입
CREATE TABLE ex2_3(
COL_INT INTEGER
, COL_DEC DECIMAL
, COL_NUM NUMBER
);

SELECT
column_id
, column_name
, data_type
, data_length
FROM user_tab_cols
WHERE table_name = 'EX2_3'
ORDER BY column_id;

-- p57
CREATE TABLE ex2_4 (
COL_FLOT1 FLOAT(32),
COL_FLOT2 FLOAT
);

INSERT INTO ex2_4 (col_flot1, col_flot2) VALUES (1234567891234, 1234567891234);

-- 조회
SELECT * FROM ex2_4;

-- p.58
CREATE TABLE ex2_5(
COL_DATE DATE
, COL_TIMESTAMP TIMESTAMP
);
INSERT INTO ex2_5 VALUES (SYSDATE, SYSTIMESTAMP);
SELECT * FROM ex2_5;

-- LOB 데이터 타입
-- Large object의 약자로 대용량 데이터 저장할 수 있는 데이터 타입
-- 비정형 데이터는 그 크기가 매우 큰데, 이런 데이터를 저장한다.
```

- Reference
    - [오라클 19c 기본 세팅 - Data Science | DSChloe](https://dschloe.github.io/sql/oracle_basic_settings/)
    - 오라클 SQL과 PL/SQL을 다루는 기술