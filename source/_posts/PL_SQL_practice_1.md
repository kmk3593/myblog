---
title: "PL/SQL practice01"
tags:
  - PL/SQL
categories:
  - SQL
  - PL/SQL
author: "minkuen"
date: '2022-05-20'
---


- PL/SQL은 일반 프로그래밍 언어에서 제공하는 많은 기능이 탑재되어 있다.
- 다른 프로그래밍 언어와 다른 점은 PL/SQL은 DB에 직접 탑재되어 컴파일되고 실행되어 성능 면에서도 우수하고, DB 관련 처리를 할 때 수많은 기능을 제공한다

### IF문

```sql
-- IF문

SET SERVEROUTPUT ON
DECLARE
    vn_num1 NUMBER := 1;
    vn_num2 NUMBER := 2;
BEGIN 
    IF vn_num1 >= vn_num2 THEN
        DBMS_OUTPUT.PUT_LINE(vn_num1 || '이 큰 수');
    ELSE
        DBMS_OUTPUT.PUT_LINE(vn_num2 || '이 큰 수');
    END IF;
END;
```

실행)

![Untitled](/images/PL_SQL_practice_1/Untitled.png)

### ELSE IF문

```sql
DECLARE 
    vn_salary NUMBER := 0; -- 변수 초기화 
    vn_department_id NUMBER := 0; -- 변수 초기화 
BEGIN
    vn_department_id := ROUND(DBMS_RANDOM.VALUE (10, 120), -1);
    SELECT salary 
        INTO vn_salary
    FROM employees
    WHERE department_id = vn_department_id
        AND ROWNUM = 1;
    
    DBMS_OUTPUT.PUT_LINE(vn_salary);
    
    IF vn_salary BETWEEN 1 AND 3000 THEN 
        DBMS_OUTPUT.PUT_LINE('낮음');
    ELSIF vn_salary BETWEEN 3001 AND 6000 THEN 
        DBMS_OUTPUT.PUT_LINE('중간');
    ELSIF vn_salary BETWEEN 6001 AND 10000 THEN 
        DBMS_OUTPUT.PUT_LINE('높음');
    ELSE
        DBMS_OUTPUT.PUT_LINE('최상위');
    END IF;
END;
```

### 중첩 IF문

```sql
-- 중첩 IF문
DECLARE 
    vn_salary NUMBER := 0;
    vn_department_id NUMBER := 0;
    vn_commission NUMBER := 0;
BEGIN 
    vn_department_id := ROUND(DBMS_RANDOM.VALUE (10,120), -1);
    SELECT salary, commission_pct
        INTO vn_salary, vn_commission
    FROM employees
    WHERE department_id = vn_department_id
        AND ROWNUM = 1;
    DBMS_OUTPUT.PUT_LINE(vn_salary);
    
    IF vn_commission > 0 THEN 
        IF vn_commission > 0.15 THEN 
            DBMS_OUTPUT.PUT_LINE(vn_salary * vn_commission);
        END IF;
    ELSE
        DBMS_OUTPUT.PUT_LINE(vn_salary);
    END IF;
END;
```

### CASE

```sql
-- CASE (p.277)
DECLARE 
    vn_salary NUMBER := 0; -- 변수 초기화 
    vn_department_id NUMBER := 0; -- 변수 초기화 
BEGIN
    vn_department_id := ROUND(DBMS_RANDOM.VALUE (10, 120), -1);
    SELECT salary 
        INTO vn_salary
    FROM employees
    WHERE department_id = vn_department_id
        AND ROWNUM = 1;
    
    DBMS_OUTPUT.PUT_LINE(vn_salary);
    
    CASE WHEN vn_salary BETWEEN 1 AND 3000 THEN 
            DBMS_OUTPUT.PUT_LINE('낮음');
        WHEN vn_salary BETWEEN 3001 AND 6000 THEN 
            DBMS_OUTPUT.PUT_LINE('낮음');
        WHEN vn_salary BETWEEN 6001 AND 10000 THEN 
            DBMS_OUTPUT.PUT_LINE('높음');
        ELSE
            DBMS_OUTPUT.PUT_LINE('최상위');
    END CASE;
END;
```

### LOOP 문

```sql
-- LOOP
-- 3단
DECLARE 
    vn_base_num NUMBER := 3;
    vn_cnt      NUMBER := 1;
BEGIN 
    LOOP
        DBMS_OUTPUT.PUT_LINE(vn_base_num || '*' || vn_cnt || '= ' 
                             || vn_base_num * vn_cnt);
        vn_cnt := vn_cnt + 1;
        
        EXIT WHEN vn_cnt > 9; -- vn_cnt가 9보다 크면 루프 종료
    END LOOP;
END;
```

### WHILE 문

```sql
-- WHILE 
DECLARE 
    vn_base_num NUMBER := 3;
    vn_cnt      NUMBER := 1;
BEGIN
-- 조건식이 참일 때만 실행되는 것
-- 조건식이 거짓이 되면 실행 중지
WHILE vn_cnt <= 9 -- vn_cnt가 9보다 크면 루프 종료
    LOOP
        DBMS_OUTPUT.PUT_LINE(vn_base_num || '*' || vn_cnt || '= ' 
                             || vn_base_num * vn_cnt);
        vn_cnt := vn_cnt + 1;
    END LOOP;
END;
```

### WHILE (EXIT)

```sql
-- WHILE (EXIT)
-- WHILE 
DECLARE 
    vn_base_num NUMBER := 3;
    vn_cnt      NUMBER := 1;
BEGIN
-- 조건식이 참일 때만 실행되는 것
-- 조건식이 거짓이 되면 실행 중지
WHILE vn_cnt <= 9 -- vn_cnt가 9보다 크면 루프 종료
    LOOP
        DBMS_OUTPUT.PUT_LINE(vn_base_num || '*' || vn_cnt || '= ' 
                             || vn_base_num * vn_cnt);
                             
        -- Break (= EXIT)
        EXIT WHEN vn_cnt = 5; -- vn_cnt값이 5가 되면 루프 종료
        vn_cnt := vn_cnt + 1;
    END LOOP;
END;
```

### FOR-LOOP

```sql
-- FOR-LOOP 
-- 인덱스값
DECLARE
    vn_base_num NUMBER := 3;
BEGIN 
    FOR i IN 1..9
    LOOP 
        DBMS_OUTPUT.PUT_LINE (vn_base_num || '*' || i || '= ' || vn_base_num * i);
    END LOOP;
END;
```

### CONTINUE

```sql
-- CONTINUE
DECLARE
    vn_base_num NUMBER := 3;
BEGIN 
    FOR i IN 1..9
    LOOP
        CONTINUE WHEN i = 5;
        DBMS_OUTPUT.PUT_LINE (vn_base_num || '*' || i || '= ' || vn_base_num * i);
    END LOOP;
END;
```

### GOTO 문

```sql
-- GOTO문
-- 사용자 정의 함수와 약간 비슷

DECLARE 
    vn_base_num NUMBER := 3;
BEGIN 
    <<third>>
    FOR i IN 1..9
    LOOP
        DBMS_OUTPUT.PUT_LINE (vn_base_num || '*' || i || '= ' || vn_base_num * i);
        IF i = 3 THEN
            GOTO fourth;
        END IF;
    END LOOP;
    
    <<fourth>>
    vn_base_num := 4;
    FOR i IN 1..9
    LOOP
        DBMS_OUTPUT.PUT_LINE (vn_base_num || '*' || i || '= ' || vn_base_num * i);
    END LOOP;
END;

-- NULL문
-- 검색 찾기 링크 참조
```

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술