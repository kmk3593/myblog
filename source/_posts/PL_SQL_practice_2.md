---
title: "PL/SQL practice02"
tags:
  - PL/SQL
categories:
  - SQL
  - PL/SQL
author: "minkuen"
date: '2022-05-21'
---

- PL/SQL은 일반 프로그래밍 언어에서 제공하는 많은 기능이 탑재되어 있다.
- 다른 프로그래밍 언어와 다른 점은 PL/SQL은 DB에 직접 탑재되어 컴파일되고 실행되어 성능 면에서도 우수하고, DB 관련 처리를 할 때 수많은 기능을 제공한다

### 프로시저

```sql
-- 프로시저
-- 함수와 다르게 로직 처리만 수행 / 결괏값 반환 (X)
-- p.290
SELECT * FROM JOBS;

-- 프로시저 생성
CREATE OR REPLACE PROCEDURE my_new_job_proc
(p_job_id IN JOBS.JOB_ID%TYPE
 , p_job_title IN JOBS.JOB_TITLE%TYPE
 , p_min_sal IN JOBS.MIN_SALARY%TYPE
 , p_max_sal IN JOBS.MAX_SALARY%TYPE
)
IS
BEGIN
    INSERT INTO JOBS(job_id
                     , job_title
                     , min_salary
                     , max_salary
                     , create_date
                     , update_date) 
    VALUES(p_job_id, p_job_title, p_min_sal, p_max_sal, SYSDATE, SYSDATE);
    
    COMMIT;
END;
```

### 프로시저 실행

```sql
-- 프로시저 실행
-- exec
EXEC my_new_job_proc ('SM_JOB1', 'Sample JOB1', 1000, 5000);

-- 확인
SELECT * 
FROM jobs
WHERE job_id = 'SM_JOB1';

-- 프로시저 업데이트 
-- 끊기면 안되고, 계속 실행이 되어야 함

CREATE OR REPLACE PROCEDURE my_new_job_proc
(p_job_id IN JOBS.JOB_ID%TYPE
 , p_job_title IN JOBS.JOB_TITLE%TYPE
 , p_min_sal IN JOBS.MIN_SALARY%TYPE
 , p_max_sal IN JOBS.MAX_SALARY%TYPE
)
IS
    vn_cnt NUMBER := 0;
BEGIN
    
    -- 동일한 JOB_ID가 있는지 체크
    SELECT COUNT(*)
        INTO vn_cnt
    FROM JOBS
    WHERE job_id = p_job_id;
    
    -- 없으면 INSERT 
    IF vn_cnt = 0 THEN 
        INSERT INTO JOBS(job_id
                     , job_title
                     , min_salary
                     , max_salary
                     , create_date
                     , update_date) 
        VALUES(p_job_id, p_job_title, p_min_sal, p_max_sal, SYSDATE, SYSDATE);
    ELSE -- 있으면 UPDATE
        UPDATE JOBS 
            SET job_title    = p_job_title
            ,   min_salary   = p_min_sal
            ,   max_salary   = p_max_sal
            ,   update_date  = SYSDATE
        WHERE job_id = p_job_id;
    END IF;
    COMMIT;
END;
```

### 프로시저 실행

```sql
-- 프로시저 실행
-- exec
EXEC my_new_job_proc ('SM_JOB1', 'Sample JOB1', 1000, 5000);

SELECT * 
FROM jobs
WHERE job_id = 'SM_JOB1';
```

```sql
-- p.293
-- 한줄로 실행. (이유 모름)
EXECUTE my_new_job_proc (p_job_id => 'SM_JOB1', p_job_title => 'Sample JOB1', p_min_sal => 2000, p_max_sal => 7000);
```

```sql
SELECT * FROM jobs WHERE job_id = 'SM_JOB1';
```

```sql
-- 매개변수 디폴트 설정
CREATE OR REPLACE PROCEDURE my_new_job_proc
(p_job_id IN JOBS.JOB_ID%TYPE
 , p_job_title IN JOBS.JOB_TITLE%TYPE
 , p_min_sal IN JOBS.MIN_SALARY%TYPE := 10
 , p_max_sal IN JOBS.MAX_SALARY%TYPE := 100
)
IS
    vn_cnt NUMBER := 0;
BEGIN
    
    -- 동일한 JOB_ID가 있는지 체크
    SELECT COUNT(*)
        INTO vn_cnt
    FROM JOBS
    WHERE job_id = p_job_id;
    
    -- 없으면 INSERT 
    IF vn_cnt = 0 THEN 
        INSERT INTO JOBS(job_id
                     , job_title
                     , min_salary
                     , max_salary
                     , create_date
                     , update_date) 
        VALUES(p_job_id, p_job_title, p_min_sal, p_max_sal, SYSDATE, SYSDATE);
    ELSE -- 있으면 UPDATE
        UPDATE JOBS 
            SET job_title    = p_job_title
            ,   min_salary   = p_min_sal
            ,   max_salary   = p_max_sal
            ,   update_date  = SYSDATE
        WHERE job_id = p_job_id;
    END IF;
    COMMIT;
END;
```

```sql
EXECUTE my_new_job_proc('SM_JOB1', 'Sample JOB1');
SELECT * FROM jobs WHERE job_id = 'SM_JOB1';
```

```sql
-- OUT, IN OUT 매개변수
CREATE OR REPLACE PROCEDURE my_new_job_proc
(p_job_id IN JOBS.JOB_ID%TYPE
 , p_job_title IN JOBS.JOB_TITLE%TYPE
 , p_min_sal IN JOBS.MIN_SALARY%TYPE := 10
 , p_max_sal IN JOBS.MAX_SALARY%TYPE := 100
 , p_upd_date OUT JOBS.UPDATE_DATE%TYPE -- 갱신일자 값을 반환한다! 
)
IS
    vn_cnt NUMBER := 0;
    vn_cur_date JOBS.UPDATE_DATE%TYPE := SYSDATE;
BEGIN
    
    -- 동일한 JOB_ID가 있는지 체크
    SELECT COUNT(*)
        INTO vn_cnt
    FROM JOBS
    WHERE job_id = p_job_id;
    
    -- 없으면 INSERT 
    IF vn_cnt = 0 THEN 
        INSERT INTO JOBS(job_id
                     , job_title
                     , min_salary
                     , max_salary
                     , create_date
                     , update_date) 
        VALUES(p_job_id, p_job_title, p_min_sal, p_max_sal, SYSDATE, SYSDATE);
    ELSE -- 있으면 UPDATE
        UPDATE JOBS 
            SET job_title    = p_job_title
            ,   min_salary   = p_min_sal
            ,   max_salary   = p_max_sal
            ,   update_date  = SYSDATE
        WHERE job_id = p_job_id;
    END IF;
    COMMIT;
END;
```

```sql
-- OUT, IN OUT 매개변수
CREATE OR REPLACE PROCEDURE my_new_job_proc
(p_job_id IN JOBS.JOB_ID%TYPE
 , p_job_title IN JOBS.JOB_TITLE%TYPE
 , p_min_sal IN JOBS.MIN_SALARY%TYPE := 10
 , p_max_sal IN JOBS.MAX_SALARY%TYPE := 100
 , p_upd_date OUT JOBS.UPDATE_DATE%TYPE -- 갱신일자 값을 반환한다! 
)
IS
    vn_cnt NUMBER := 0;
    vn_cur_date JOBS.UPDATE_DATE%TYPE := SYSDATE;
BEGIN
    
    -- 동일한 JOB_ID가 있는지 체크
    SELECT COUNT(*)
        INTO vn_cnt
    FROM JOBS
    WHERE job_id = p_job_id;
    
    -- 없으면 INSERT 
    IF vn_cnt = 0 THEN 
        INSERT INTO JOBS(job_id
                     , job_title
                     , min_salary
                     , max_salary
                     , create_date
                     , update_date) 
        VALUES(p_job_id, p_job_title, p_min_sal, p_max_sal, vn_cur_date, vn_cur_date);
    ELSE -- 있으면 UPDATE
        UPDATE JOBS 
            SET job_title    = p_job_title
            ,   min_salary   = p_min_sal
            ,   max_salary   = p_max_sal
            ,   update_date  = vn_cur_date
        WHERE job_id = p_job_id;
    END IF;
    
    -- OUT 매개변수에 갱신 일자 할당
    p_upd_date := vn_cur_date;
    COMMIT;
END;

SET SERVEROUTPUT ON
DECLARE 
    vd_cur_date JOBS.UPDATE_DATE%TYPE; 
BEGIN 
    my_new_job_proc('SM_JOB1', 'Sample JOB1', 2000, 6000, vd_cur_date);
    DBMS_OUTPUT.PUT_LINE(vd_cur_date);
END;
```

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술