---
title: "Oracle_practice3"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-07'
---

### sql developer

- sql developer에서 새로운 sql 워크시트를 생성한다.
    
    도구 → sql워크시트 : 
    
- 오라클 SQL과 PL/SQL을 다루는 기술 92p

### SELECT 사용법

- 교재를 참고하여 코드를 익혀보자
- SELECT문은 다음과 같이 사용한다.

```sql
-- SELECT
SELECT * 혹은 컬럼
FROM 테이블 또는 VIEW
WHERE 조건
ORDER BY 컬럼;

어디서 가져올 것인가? FROM
무얼을 가져올 것인가? SELECT
어떻게 가져올 것인가? WHERE
```

### SELECT 문

- SELECT문을 실제로 사용해본다.

```sql
-- SELECT
-- 질문 : 사원 테이블에서 급여가 5000이 넘는 사원번호와 사원명을 조회한다.
DESC employees;

SELECT 
    employee_id
    , emp_name
    , salary
FROM employees
WHERE salary > 5000;
```

- 다음과 같이 출력된다.

![Untitled](/images/Oracle_practice_3/Untitled.png)

- select문을 좀 더 다양하게 작성해본다.

```sql
-- 급여가 5000 이상이고 job_id가 IT_PROG 사원 조회
-- 94p
SELECT 
    employee_id
    , emp_name
    , salary
FROM employees
WHERE salary > 5000
    AND job_id = 'IT_PROG'
ORDER BY employee_id;
```

![Untitled](/images/Oracle_practice_3/Untitled%201.png)

### INSERT문, SELECT문

- INSERT문으로 행을 삽입하고 SELECT로 출력해보자.

```sql
-- p.94
-- 급여가 5000 이상이고 job_id가 IT_PROG 사원 조회
SELECT 
    employee_id
    , emp_name
    , salary
FROM employees
WHERE salary > 5000
    AND job_id = 'it_prog' -- 영어는 대소문자 구분
ORDER BY employee_id;

-- 급여가 5000 이상이거나 job_id가 'IT_PROG'인 사원 (OR)
-- 합집합
SELECT 
    employee_id
    , emp_name
    , salary
    , job_id
FROM employees
WHERE salary > 5000
    OR job_id = 'it_prog' -- 영어는 대소문자 구분
ORDER BY employee_id;

SELECT * FROM employees;

-- INSERT 
CREATE TABLE ex3_1 (
    col1 VARCHAR2(10), 
    col2 NUMBER, 
    col3 DATE
);

INSERT INTO ex3_1(col1, col2, col3) 
VALUES ('ABC', 10, SYSDATE);

-- 컬럼 순서를 바꿔도 큰 문제가 안됨
INSERT INTO ex3_1(col3, col1, col2)
VALUES (SYSDATE, 'DEF', 20);

SELECT * FROM ex3_1;

-- 타입 맞추지 않음 오류 발생
INSERT INTO ex3_1(col1, col2, col3)
VALUES ('ABC', 10, 30);

-- p.97
-- 컬럼명 생략
INSERT INTO ex3_1
VALUES ('GHI', 10, SYSDATE);

INSERT INTO ex3_1 (col1, col2)
VALUES('GHI', 20);

SELECT * FROM ex3_1;
```

![Untitled](/images/Oracle_practice_3/Untitled%202.png)

- 자주 사용되는 SELECT문 활용법이다.

```sql
-- p.98
CREATE TABLE ex3_2(
    emp_id      NUMBER
    , emp_name  VARCHAR2(100)
);

-- 실무에서 많이 쓰임
INSERT INTO ex3_2(emp_id, emp_name) 
SELECT
    employee_id
    , emp_name
FROM employees
WHERE salary > 5000;

SELECT * FROM ex3_2;
```

![Untitled](/images/Oracle_practice_3/Untitled%203.png)

### UPDATE 문 사용법

- UPDATE : 기존 데이터를 수정
- ARTER : 기존 테이블의 컬럼명 수정, 제약조건

```sql
UPDATE 테이블명
SET 컬럼1 = 변경값1, 컬럼2 = 변경값2
WHERE 조건;
```

### UPDATE 문

- UPDATE 문을 실제로 사용해보자.

```sql
SELECT * FROM ex3_1;

-- col2 모두 50으로 변경한다.
UPDATE ex3_1
SET col2 = 50;

SELECT * FROM ex3_1;
```

- col2 값이 모두 50으로 수정되었다.

![Untitled](/images/Oracle_practice_3/Untitled%204.png)

- SELECT문으로 사람 이름을 수정해보자.

```sql
UPDATE ex3_2
SET EMP_NAME = 10 -- Michael Hartstein
WHERE EMP_ID = 201;

SELECT * FROM ex3_2;
```

- Michael이란 이름이 10으로 변경되었다.

![Untitled](/images/Oracle_practice_3/Untitled%205.png)

### MERGE

- 조건 비교해서 테이블에 해당 조건에 맞는 데이터가 없으면 INSERT 있으면 UPDATE하는 방식이다.

```
MERGE INTO [스키마.]테이블명
        USING (update나 insert될 데이터 원천)
             ON (update될 조건)
    WHEN MATCHED THEN
           SET 컬럼1 = 값1, 컬럼2 = 값2, ...
    WHERE update 조건
           DELETE WHERE update_delete 조건
    WHEN NOT MATCHED THEN
           INSERT (컬럼1, 컬럼2, ...) VALUES (값1, 값2,...)
           WHERE insert 조건;
```

```sql
-- MERGE
-- 조건 비교해서 테이블에 해당 조건에 맞는 데이터가 없으면 INSERT
-- 있으면 UPDATE

CREATE TABLE ex3_3(
    employee_id     NUMBER
    , bonum_amt     NUMBER DEFAULT 0
);

SELECT * FROM SALES;
DESC SALES;

-- ex3_3 신규테이블 생성
INSERT INTO ex3_3(employee_id)
SELECT 
    e.employee_id
FROM employees e, sales s 
WHERE e.employee_id = s.employee_id
    AND s.SALES_MONTH BETWEEN '200010' AND '200012'
GROUP BY e.employee_id;
-- group by를 통해 중복 제거

SELECT * FROM ex3_3 ORDER BY employee_id;

```

![Untitled](/images/Oracle_practice_3/Untitled%206.png)

### 서브쿼리

- 쿼리 안에 또 다른 쿼리가 있는 형태이다.

```sql
-- (1) 관리자 사번(manager_id)이 146번인 사원을 찾는다.
-- (2) ex3_3 테이블에 있는 사원의 사번과 일치하면
--     보너스 금액에 자신의 급여의 1%를 보너스로 갱신
-- (3) ex3_3 테이블에 있는 사원의 사번과 일치하지 않으면
--      (1)의 결과의 사원을 신규로 입력 (이 때 보너스 금액은 급여의 0.1%
-- (4) 이 때 급여가 8000미만인 사원만 처리해보자.

-- 서브쿼리
SELECT
    employee_id
    , manager_id
    , salary
    , salary * 0.01 -- 10%
FROM employees
WHERE employee_id IN (SELECT employee_id FROM ex3_3);
```

![Untitled](/images/Oracle_practice_3/Untitled%207.png)

- 서브쿼리의 또 다른 예시이다.

```sql
-- 관리자 사번이 146번인 사원은 161번 사원 한 명이므로
-- ex3_3 테이블에서 161인 건의 보너스 금액은 7,000 * 0.01, 즉 70으로 갱신

SELECT
    employee_id
    , manager_id
    , salary
    , salary * 0.01 -- 10%
FROM employees
WHERE employee_id NOT IN (SELECT employee_id FROM ex3_3)
    AND manager_id = 146;
```

![Untitled](/images/Oracle_practice_3/Untitled%208.png)

### MERGE 문

```sql
MERGE INTO ex3_3 d 
    USING (SELECT
                employee_id
                , salary 
                , manager_id
           FROM employees
           WHERE manager_id = 146) b 
        ON (d.employee_id = b.employee_id)
WHEN MATCHED THEN 
    UPDATE SET d.bonus_amt = d.bonus_amt + b.salary * 0.01 
WHEN NOT MATCHED THEN 
    INSERT (d.employee_id, d.bonus_amt) VALUES (b.employee_id, b.salary * 0.001)
    WHERE (b.salary < 8000);
    
SELECT * FROM ex3_3 ORDER BY employee_id;
```

- 오타 처리하다 3번 실행한 결과이다.

![Untitled](/images/Oracle_practice_3/Untitled%209.png)

### DELETE 문

- UPDATE에 비해 간단하다.
- 삭제하기만 하면 되기 때문.

```sql
-- DELETE 문
-- 106p
DELETE ex3_3;
SELECT * FROM ex3_3;
```

### COMMIT, ROLLBACK

- commit과 rollback을 사용해보자.

```sql
-- Commit Rollback Truncate
-- Commit : 변경한 데이터를 DB에 마지막으로 반영
-- ROLLBACK : 반대로 변경한 데이터를 변경하기 이전 상태로 되돌림
CREATE TABLE ex3_4 (
    employee_id NUMBER 
);
    
INSERT INTO ex3_4 VALUES (100);

SELECT * FROM ex3_4;

commit;
rollback;
```

![Untitled](/images/Oracle_practice_3/Untitled%2010.png)

- commit 후에는, sqlplus에서도 테이블을 출력 할 수 있게 된다.

![Untitled](/images/Oracle_practice_3/Untitled%2011.png)

### TRUNCATE문

- 한번 실행 시, 데이터 바로 삭제한다.
- ROLLBACK 적용 안됨

```sql
-- TRUNCATE 문
-- 한번 실행시, 데이터 바로 삭제, ROLLBACK 적용 안됨
-- DELETE문은 데이터 삭제 후, COMMIT 필요 / ROLLBACK 데이터가 삭제되기 전의 복구 불가

SELECT * FROM ex3_4;
TRUNCATE TABLE ex3_4;
```

![Untitled](/images/Oracle_practice_3/Untitled%2012.png)

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술