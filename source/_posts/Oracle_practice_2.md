---
title: "Oracle_practice2"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-06'
---


### sql developer

- sql developer에서 새로운 sql 워크시트를 생성한다.
    - 도구 → sql 워크시트 : ch02_0426
- 오라클 SQL과 PL/SQL을 다루는 기술 60p

### 실습

- 교재를 참고하여 코드를 익혀보자
- 제약조건을 작성해본다.

```sql
-- 60P
-- not null
-- 제약 조건
CREATE TABLE ex2_6(
    COL_NULL        VARCHAR2(10)
    , COL_NOT_NULL  VARCHAR2(10) NOT NULL
);

INSERT INTO ex2_6 VALUES ('AA', '');
INSERT INTO ex2_6 VALUES ('AA', 'BB');

SELECT * FROM ex2_6;

-- USER CONSTRAINTS 제약 조건 확인
SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_6';

```

- SELECT 문을 사용하여 제약 조건을 출력.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled.png)

- 이어서 실습한다.

```sql

-- UNIQUE
-- 중복값 허용 안 함
CREATE TABLE ex2_7 (
    COL_UNIQUE_NULL VARCHAR2(10) UNIQUE
    , COL_UNIQUE_NULL VARCHAR2(10) UNIQUE NOT NULL
    , COL_UNIQUE VARCHAR(10)
    , CONSTRAINTS unique_nm1 UNIQUE (COL_UNIQUE)
);

SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_7';
 
 SELECT * FROM ex2_7;
 
 INSERT INTO ex2_7 VALUEs('AA', 'AA', 'AA');
 SELECT * FROM ex2_7;
 
 INSERT INTO ex2_7 VALUES('AA', 'AA', 'AA');
 SELECT * FROM ex2_7;
 
 INSERT INTO ex2_7 VALUES('', 'BB', 'BB');
 INSERT INTO ex2_7 VALUES('', 'CC', 'CC');
 SELECT * FROM ex2_7;

-- 기본키 ( 63P)
CREATE TABLE ex2_8(
    COL VARCHAR2(10) PRIMARY KEY
    , COL2 VARCHAR2(10)
);

SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_8';
 
INSERT INTO ex2_8 VALUES('','AA');
-- 오류 보고 ORA-01400: NULL을 ("ORA_USER"."EX2_8"."COL") 안에 삽입할 수 없습니다
-- NULL 값을 삽입하여 생기는 오류이다. NULL값 대신 다른 값을 입력하자.
```

- 여기까지 입력하고 실행하면 오류가 발생한다.

— 오류 보고 ORA-01400: NULL을 ("ORA_USER"."EX2_8"."COL") 안에 삽입할 수 없습니다

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%201.png)

- NULL 값을 삽입하여 생기는 오류이다. NULL값 대신 다른 값을 입력하자.

```sql
-- 오류 보고 ORA-01400: NULL을 ("ORA_USER"."EX2_8"."COL") 안에 삽입할 수 없습니다
-- NULL 값을 삽입하여 생기는 오류이다. NULL값 대신 다른 값을 입력하자.
INSERT INTO ex2_8 VALUES('AA','AA');
SELECT * FROM ex2_8;
```

- 이번에는 오류가 출력되지 않았다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%202.png)

- 같은 값을 다시 입력해보자.

```sql
INSERT INTO ex2_8 VALUES('AA','AA');
-- ORA-00001: 무결성 제약 조건(ORA_USER.SYS_C007484)에 위배됩니다
-- 값이 같은 데이터를 입력하여 생기는 오류이다. 다른 데이터를 입력해야 한다.

```

- 오류가 발생했다.

-- ORA-00001: 무결성 제약 조건(ORA_USER.SYS_C007484)에 위배됩니다

- 값이 같은 데이터를 입력하여 생기는 오류이다. 다른 데이터를 입력하면 해결된다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%203.png)

### 테이블 생성과 제약조건

- 90p의 테이블을 생성해보자.

```sql
-- 90p 테이블 1, 2, 3번 생성
CREATE TABLE ORDERS (
    ORDER_ID              NUMBER(12, 0)
    , ORDER_DATE          DATE
    , ORDER_MODE          VARCHAR2(8 BYTE)
    , CUSTOMER_ID         NUMBER(6, 0)
    , ORDER_STATUS        NUMBER(2, 0)
    , ORDER_TOTAL         NUMBER(8, 2) DEFAULT 0
    , SALES_REP_ID        NUMBER(6, 0)
    , PROMOTION_ID        NUMBER(6, 0)
    , CONSTRAINT PK_ORDER PRIMARY KEY (ORDER_ID)
    , CONSTRAINT CK_ORDER_MODE CHECK (ORDER_MODE in ('direct', 'online'))
);

CREATE TABLE ORDER_ITEMS (
           ORDER_ID	    NUMBER(12,0),
           LINE_ITEM_ID NUMBER(3,0) ,
           ORDER_MODE	  VARCHAR2(8 BYTE),
           PRODUCT_ID   NUMBER(3,0), 
           UNIT_PRICE   NUMBER(8,2) DEFAULT 0, 
           QUANTITY     NUMBER(8,0) DEFAULT 0,
           CONSTRAINT PK_ORDER_ITEMS PRIMARY KEY (ORDER_ID, LINE_ITEM_ID)
); 

CREATE TABLE PROMOTIONS (
           PROMO_ID	    NUMBER(12,0),
           PROMO_NAME	  VARCHAR2(8 BYTE),
           CONSTRAINT PK_PROMOTIONS PRIMARY KEY (PROMO_ID)
); 

-- CHECK
CREATE TABLE ex2_9 (
    num1     NUMBER 
        CONSTRAINTS check1 CHECK ( num1 BETWEEN 1 AND 9),
    gender   VARCHAR2(10) 
        CONSTRAINTS check2 CHECK ( gender IN ('MALE', 'FEMALE'))        
); 

SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_9';
 
INSERT INTO ex2_9 VALUES (10, 'MAN');
INSERT INTO ex2_9 VALUES (5, 'FEMALE');
```

### 테이블 삭제

```sql
-- DEFAULT 
-- PL/SQL 사용하면 편하게 해결 가능
DROP TABLE ex2_10;

CREATE TABLE ex2_10 (
   Col1        VARCHAR2(10) NOT NULL, 
   Col2        VARCHAR2(10) NULL, 
   Create_date DATE DEFAULT SYSDATE
);
   
-- Col1 Col2 사용자가 입력
-- Create_Date DB에서 자동으로 입력
INSERT INTO ex2_10 (col1, col2) VALUES ('AA', 'BB');
SELECT * FROM ex2_10; 
```

- 여기까지 작성하고 실행하면 다음과 같이 출력된다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%204.png)

### 테이블 변경

- 이번엔 테이블을 여러 명령어를 통해 다뤄보자

```sql

-- 테이블 변경
-- 69p (1) 컬럼명 변경

ALTER TABLE ex2_10 RENAME COLUMN Col1 TO Col11;
SELECT * FROM ex2_10;

DESC ex2_10;

-- (2) 컬럼 타입 변경
-- 컬럼 타입 변경 (VARCHAR2(10) ~ VARCHAR2(30))으로 변경
ALTER TABLE ex2_10 MODIFY Col2 VARCHAR2(30);
DESC ex2_10;
```

- 테이블이 변경된다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%205.png)

- 이번엔 생성하거나 삭제해본다.

```sql
-- (3) col3 NUMBER 타입으로 신규 생성
ALTER TABLE ex2_10 ADD Col3 NUMBER;
DESC ex2_10;

-- (4) 컬럼삭제
ALTER TABLE ex2_10 DROP COLUMN Col3;
DESC ex2_10;

-- 제약조건 추가
ALTER TABLE ex2_10 ADD CONSTRAINTS pk_ex2_10 PRIMARY KEY (col11);

-- USER CONSTRAINTS 제약 조건 확인
SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_10';
```

- 제약조건이 추가되었다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%206.png)

- 제약조건을 삭제해보자.

```sql
-- 제약조건 삭제
 ALTER TABLE ex2_10 DROP CONSTRAINTS pk_ex2_10;
 
 -- USER CONSTRAINTS 제약 조건 확인
SELECT constraint_name, constraint_type, table_name, search_condition
  FROM user_constraints
 WHERE table_name = 'EX2_10';
```

- 이전에 추가한 제약조건이 삭제되었다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%207.png)

### 뷰(view)

- emp_dept_v1 뷰를 생성한다.

```sql
SELECT 
    a.employee_id
    , a.emp_name
    , a.department_id -- 부서명 컬럼
    , b.department_name
FROM 
    employees a
    , departments b
WHERE a.department_id = b.department_id;

CREATE OR REPLACE VIEW emp_dept_v1 AS 
SELECT 
    a.employee_id
    , a.emp_name
    , a.department_id
    , b.department_name
FROM 
    employees a
    , departments b
WHERE a.department_id = b.department_id;
```

- 새로운 view가 생성된다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%208.png)

### 인덱스(index)

- 인덱스를 생성한다.

```sql
-- 인덱스 생성
-- 75p
-- 추후 공부해야 할 내용 : 인텍스 내부 구조에 따른 분류
---- (초중급 레벨) B-Tree 인덱스, 비트맵 인덱스, 함수 기반 인덱스
---- DB 성능
-- 인덱스 생성
-- col11 값에 중복 값을 허용하지 않는다.
-- 인덱스 생성 시, user_indexes 시스템 뷰에서 내역 확인
CREATE UNIQUE INDEX ex2_10_ix011 
ON ex2_10(col11);

SELECT index_name, index_type, table_name, uniqueness
FROM user_indexes
WHERE table_name = 'EX2_10';
```

- 실제로 인덱스가 생성되었다는 안내문이 출력된다.

![Untitled](Oracle%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B802%20fda6c62cd239487d913a661f31483873/Untitled%209.png)

- Reference :  오라클 SQL과 PL/SQL을 다루는 기술