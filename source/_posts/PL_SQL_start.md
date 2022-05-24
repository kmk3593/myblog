---
title: "PL/SQL start"
tags:
  - PL/SQL
categories:
  - SQL
  - PL/SQL
author: "minkuen"
date: '2022-05-19'
---


### PL/SQL

- SQL은 비절차적 언어
    - 파이썬, R, 자바 등과는 다르다
- ‘DB 프로그래밍’이라 하면 SQL을 사용한 DML문을 사용하는 것을 지칭할 수도 있지만, 실제 복잡한 비즈니스 로직을 만드는 것은 PL/SQL을 사용해 구현하는 것이 보통이다.
- PL/SQL은 일반 프로그래밍 언어에서 제공하는 많은 기능이 탑재되어 있다.
- 다른 프로그래밍 언어와 다른 점은 PL/SQL은 DB에 직접 탑재되어 컴파일되고 실행되어 성능 면에서도 우수하고, DB 관련 처리를 할 때 수많은 기능을 제공한다.

둘째 마당 

- 복잡한 비즈니스 로직을 처리하는 —> 프로그래밍


### PL/SQL 기본 구조

- PL/SQL 소스 프로그램의 기본 단위를 **블록**(Block)이라고 하는데, 블록은 선언부, 실행부, 예외 처리부로 구성된다.
- 이 블록은 다시 이름이 없는 블록과 이름이 있는 블록으로 구분할 수 있는데 전자에 속하는 것이 익명 블록이며, 함수, 프로시저, 패키지 등이 후자에 속한다.
- 오라클 SQL과 PL/SQL을 다루는 기술 260p

- 이름이 없는 익명 블록anonymous block을 사용해 PL/SQL 코드를 작성해 보자.
- 먼저 변수를 선언하고 값을 할당해 이 값을 출력하는 익명 블록을 만든다.

```sql
-- PL/SQL
-- 블록 단위로 진행
-- 선언부
SET SERVEROUTPUT ON
SET TIMING ON       -- 경과시간 확인
DECLARE
    vi_num NUMBER;  -- 변수 선언
BEGIN
    -- 실행 (코드 실행)
    vi_num := 100;
    DBMS_OUTPUT.PUT_LINE(vi_num);
END; -- 블록 종료
-- / PL/SQL 자체가 종료
```

- 만약 현재 로그온 한 SQL*Plus를 종료하고 다시 접속한다면 “SET SERVEROUTPUT ON”이란 명령어를 다시 실행해야 출력 결과를 볼 수 있다.*
- *참고로 SQL*Plus 상에서 PL/SQL 블록을 실행했을 때 총 소요시간도 알 수 있는데, 이를 위해서는 SET TIMING ON 명령어를 실행하면 된다.

실행)

![Untitled](/images/PL_SQL_start/Untitled.png)

### 상수

- 상수는 변수와는 달리 한 번 값을 할당하면 변하지 않는다
- `상수명 CONSTANT 데이터타빙 : = 상수값;`

```sql
-- p.264
DECLARE
    a INTEGER := 2**2*3**2; -- 4 * 9
BEGIN
    DBMS_OUTPUT.PUT_LINE('a = ' || TO_CHAR(a));
END;
```

실행)

![Untitled](/images/PL_SQL_start/Untitled%201.png)

### DML문

- SQL문 중 DDL은 PL/SQL 상에서 직접 쓸 수 없고 DML문만 사용한다.

```sql
-- DM문
-- PL/SQL 테이블과 연동해서 특정 로직을 처리하는 것

DECLARE
    vs_emp_name VARCHAR2(80); -- 사원명 변수
    vs_dep_name VARCHAR2(80); -- 부원명 변수
BEGIN
    SELECT a.emp_name, b.department_name
        INTO vs_emp_name, vs_dep_name
    FROM employees a
        , departments b
    WHERE a.department_id = b.department_id
        AND a.employee_id = 100;
    DBMS_OUTPUT.PUT_LINE(vs_emp_name || ' - ' || vs_dep_name);
END;
```

실행)

![Untitled](/images/PL_SQL_start/Untitled%202.png)

### 데이터 타입

```sql
DECLARE
    vs_emp_name employees.emp_name%TYPE; -- 사원명 변수
    vs_dep_name departments.department_name%TYPE; -- 부원명 변수
BEGIN
    SELECT a.emp_name, b.department_name
        INTO vs_emp_name, vs_dep_name
    FROM employees a
        , departments b
    WHERE a.department_id = b.department_id
        AND a.employee_id = 100;
    DBMS_OUTPUT.PUT_LINE(vs_emp_name || ' - ' || vs_dep_name);
END;
```

실행)

![Untitled](/images/PL_SQL_start/Untitled%203.png)

### 데이터 크기

```sql
-- SQL과 PL/SQL에서 사용할 수 있는 데이터 크기는 다름
-- PL/SQL > SQL보다 더 큰 크기로 사용 가능
DROP TABLE ch08_varchar2;
CREATE TABLE ch08_varchar2(
    VAR1 VARCHAR2(4000)
);

INSERT INTO ch08_varchar2 (VAR1)
VALUES ('tQbADHDjqtRCvosYCLwzbyKKrQCdJubDPTHnzqvjRwGxhQJtrVbXsLNlgeeMCemGMYpvfoHUHDxIPTDjleABGoowxlzCVipeVwsMFRNzZYgHfQUSIeOITaCKJpxAWwydApVUlQiKDgJlFIOGPOKoJsoemqNbOLdZOBcQhDcMLXuYjRQZDIpgpmImgiwzcLkSilCmLrSbmFNsKEEpzCHDylMvkYPKPNeuJxLvJiApNCYzrMcflECbxwNTKSxaEwVvCYnTnFfMFgDqxobWcSmMJrNTQIVOeWlPaMTfRHsrlFSukppmljmOojPSgJiSbQcgtWWOwUNNYFGtgCGBsIcTGAiHWBxtYVXecoJgJCAJptIVmVTZSKliRLoPYTIUpksBuQaqFHLhCkosWChoMjbqgLtBIRBynsKjKiLrdeHVvZanNVElDjLWwlCDhbpsAVQMTzjzhoKIJBdthynMBMVjeNmsKAjdAYhPZKmuKOuMloQdkqPjoKbfjDEeATciMrXiMQorMhYmBlMODBbyLLIkbmtZdPcWGSuxFEUwXnWpvnunEgcLelSneRIpgRNTzTkHqgLbpxoHzCYgSWlIAvKljCnmWiPWGGwlUFOudRSdoqUxntyhNYEiVXtMObywEltTImawnElpmeiWwlTjGTFceqyjhNqiDLxwduubykWzDmFSJNvVvDZibrCpAReqQjlQZcxuVqjKGKvoDuEcQPQeDzmdMYSOTIQdPDNfDffCOUWflHSQhvVTiYumBQIoyznWNITGZkefknJpGEutUnhBgLPQTWTBeTYccqlLrxvRjfJpdpfVDqqfKCngemIEDDHNdvBxCqKDTrrJAumXMKgpWLIHctQuACeNaKnffpYXiioLxZDrxpuZPPUGpRsCtoQuBfogkKuusVATkMyajKTPSyTQbfhZepRjNdrhkymqKvsAcThYbMSMnkKcLWFPAMeGysBVKkQtFMPvRBoDszlSZcMYzwxkKQwJnuVnDxShYiHFlzgDWqhZoqeypyFVBNDtHkiVzHkQisYLbsbVneJyHbHdtaIFLVbfTqbkGQTEjFlPiGUddPUIoLWALrbKcLwBizwhJvaXkvOphcGWpdNAhxgehCvjcQFSFhxrBuANKjyWncWAUpKKJcfQCsQlLfpqdMhjWGkAMMWUaDfCrGtmtkiIZOdNapEnvfFKiHAhBhejgKSuyKXFQXyCaLwwvonHsceJKgjtnYVZvBCYYBSqNCqVqCGewootJJsqrCnmiteMZBbyMPnIrdcielnGUYmwiOPmEqKGvxDmDRTDRumnSRcnvgxLbaiQIuzdslEIMquvvwmvgaumqPkduNyfRtXErCPvDYLelhjNNOjbGryRpTtDHxIJebMEtKryUyZRIdADeTEBExwHMRHzAYFizYiesaMhNIsOUzUTmyEMuFQrsUEtjwhUWIvADNlrcxPZwRazPMMvdVZssmXbXuCkRoPYNGLPwUmrWrrIgQoMSGMPvTcbHnbtleyKYmOMgymANQBZDMoqAOzMHrAVunIiykCudFVNObNgXOoyfQRICbFsWygSZXufipvrWWmRnBWYdoKmIRewOObUjiNDdQsxQIXtlbPSSngfQPfeQKOolVASXIuAmeODKtSOPaEaFKcedGzzsbrPlsPnRRuYFeVdhyufpjFVVrTPczSQkmPYXercLMmVEaDmJXKTqEVNSKeOshDCDJwdINFsLhAuKIIfOdjSEndDwumQLvePVjzNoIfUELOANeshoNgwVhFADjtUIjIhQAIyRnzSoxSRSWklITMgdjQZTthwsnBVLWyfSsAdLzOnEqmMCGBlTYGjtqvKbBoATRwkPkOTSbUhZClVzjiLLIFEMuptuodeRKXUaBfUhVTtasFsZdVnKtEfLldJYsxjlrBADRqhEBEmBKxlXKgEhiKcwAdztcETMUteJwadfaZLEBRjwJOGaIMhsfAxtuBQWyQLGXPDlFQmkcMsKsGUlQBEAubDqbuBYqXLZgmhPftLkYaCYGReLCVXssOxzJFJwnxKJzaaYzfVpbHYBtiBeQZRilJZqrrMTrVtYAcwGxAAddwtlxzdZebfZHjzqRmrrBPNbkVHqjCHtVKUjIDPVSrtyEsPRPoyyPOFOSBcgClTzlAIPmPMkdlpFHctzKGpyQMInMwPKojVErCOrHbCsZoEXqyOcHReSybmxwYabyioVnDxPEvskutVHLWQTNudmKICoaoSGKqONrBmvtGNBKAaJxCRKTDOIqrJOsQVOmGxmuIDEddVYvDwILTyushOAiXbkRIKgNLnFJdOagmiOHKRBKIIkxkOUeZWMRNlqpJdFgKjrGhIzrgBtgjVOtZAskKRbqzRVwLUoUAtRpRkoRQNLIrbLmmjZTugXJBNCscnMguKVAFDKpODtCsmdlBvQGALeBGUitYBxLYhJxeVcAnTWmTAvCITzdzqiBfEudEIBmkDAXIFmoOmsTMZDOnhXYrgMDlDbjednYWWJbGhrXFrxMQmQSmRBwoOqWGbGmjZNlJCvSHvmtZUkIScWXVdfSsdvdyQNpGFIOuteXhCMLmmEHrMucEmFbCIOHTJINAuIUOPfAfijIPkZjppGCCSRJNXWNCmliwUgABkHWuelUWeLsyVKVcZWOSeiQBQibCQJQUgGkTrXZxdBLsgjeMIwOyORDBpywuvlrLScRNhvaCYaKKRvOZeqBebUWWFhNnIRJvedFNfFPgWZJgNRaUpyYWFNiXJfAqNjyCEQYwAdFBQKKolwrufmJOfrToJFEsoNjaphcNvfWGIjKrKZSoSJEsbRqNVcoprpcGrnBgcNAnWUFpRldcPJkPfaoLKRCmVyMAWMXmnScodKisCTqllZEWQQSCFETxLNntgdcFEFRsTSIhuewwrHIlOeCcRqkzgQhKnKyHZHdFsMEKvPywLbjaspVxUMEkVzCGcGoTmaBjUMwJuAYdSTaYGDHHWDrvGgMVTtehpzfgofkmqtamffJbCKOzJgPsHNEnFarjADJGyKLwwitCiBXIraUdZtZwNjUtGbWqxksepVYztIBrimByoYQfUQgOndzFmhnuSmhYWvHliWUHgbvBIkYasDElNsjcCLtMvjQEhJjWvlnAscPwOYfelrfgfRAZGBxdFlMNkfYEWLbkfUhbRPHoDZsaAQdoKhAAWzOcHoAkkHPQMNIxgHNJaqEFBqCuMYEtLpMnIiMCWWEPnBYgYrxlXFGYpQWUNFevwcEUvUzDeSZNrdmahAfjeLSAGjHVnqyTzJkiVXjDJXzOiszXQCErQwwDMMqjLxWebJwNAVdrXeyMDRYXmLMDnuWLVaShVGhlgvbjOdOnhCDTNVazYDnzstqxjOuWbLcDaavRumKUOQXBQwKtdFgOzXiQKWFporrIcylIHlTmTKAIpBqNUbkajLTlwAHieCcqPIJYhegwQhWpYZdfxpQXDKtYzsrmnvdiTKgXfXKlIHPHlxQtqXGhMVPOBAKVZJfkrDNEwnQFwgfoHJSqQxTzRswVLrtFgpVzKcLilgznElWUfhERyeUrCcFCuGJddlFHJrXsqRdUjqUwaBmJVNwjRbCFiVMOSFuNctNVzhmhUpoddsMPUFMvNIMsMjHIWYiLjhSajZqpDkMvUOUCbYKfNHGpdUeWGUtDXHDNSCEXqYrhWhvnISnjfoBMCwwptksarPImRZaRxBMjoBdlmRGlIuQZDzCLnxxioATnGVFFTATUpeypOCaCeJAvPLxEXYzlCgXvXirGSZFyZPPSCdOSHxeELRsetFrWgqPNNpwgbgBEYPOSpLWeVdqOxPaQnidyPVMmELzeJPWgNsWBdPJPjhkdGpeAYZfrBNqdbOwzbtLiWMPafjgWQNcWKqmcleWLcMJoGSAEIUyFuzElZKXonHOMDdGMtSKEFUWdfPfnDecKNhIjAKRYmkXgpPAzlKIOpViZPkZdozzAoWwDnXkfDikvkXcQaoBtzKkcRhNpJRYaGTkdnlfotsJZsLqpYaWoK');

commit;
    
DECLARE
   vs_sql_varchar2   VARCHAR2(4000);
   vs_plsql_varchar2 VARCHAR2(32767);
BEGIN

    -- ch08_varchar2 테이블의 값을 변수에 담는다. 
    SELECT VAR1 
        INTO vs_sql_varchar2
    FROM ch08_varchar2;
     
    -- PL/SQL 변수에 4000 BYTE 이상 크기의 값을 넣는다. 
    vs_plsql_varchar2 := vs_sql_varchar2 || ' - ' || vs_sql_varchar2 || ' - ' || vs_sql_varchar2;
  
    -- 각 변수 크기를 출력한다. 
    DBMS_OUTPUT.PUT_LINE('SQL VARCHAR2 길이 : ' || LENGTHB(vs_sql_varchar2)); 
    DBMS_OUTPUT.PUT_LINE('PL/SQL VARCHAR2 길이 : ' || LENGTHB(vs_plsql_varchar2)); 
END;
```

![Untitled](/images/PL_SQL_start/Untitled%204.png)

### 두 수의 합

```sql
-- 두 수의 합
accept p_num1 prompt '첫번째 숫자를 입력하세요 ~ '
accept p_num2 prompt '두번째 숫자를 입력하세요 ~ '

DECLARE
    v_sum number(10);
BEGIN
    v_sum := &p_num1 + &p_num2;
    DBMS_OUTPUT.PUT_LINE('TOtal : ' || v_sum);
END;
```

실행) 1 2

![Untitled](/images/PL_SQL_start/Untitled%205.png)

### 데이터 입력

```sql
DROP table emp;
DROP table dept;

CREATE TABLE DEPT
       (DEPTNO number(10),
        DNAME VARCHAR2(14),
        LOC VARCHAR2(13) );

INSERT INTO DEPT VALUES (10, 'ACCOUNTING', 'NEW YORK');
INSERT INTO DEPT VALUES (20, 'RESEARCH',   'DALLAS');
INSERT INTO DEPT VALUES (30, 'SALES',      'CHICAGO');
INSERT INTO DEPT VALUES (40, 'OPERATIONS', 'BOSTON');

CREATE TABLE EMP (
 EMPNO               NUMBER(4) NOT NULL,
 ENAME               VARCHAR2(10),
 JOB                 VARCHAR2(9),
 MGR                 NUMBER(4) ,
 HIREDATE            DATE,
 SAL                 NUMBER(7,2),
 COMM                NUMBER(7,2),
 DEPTNO              NUMBER(2) );

INSERT INTO EMP VALUES (7839,'KING','PRESIDENT',NULL,'81-11-17',5000,NULL,10);
INSERT INTO EMP VALUES (7698,'BLAKE','MANAGER',7839,'81-05-01',2850,NULL,30);
INSERT INTO EMP VALUES (7782,'CLARK','MANAGER',7839,'81-05-09',2450,NULL,10);
INSERT INTO EMP VALUES (7566,'JONES','MANAGER',7839,'81-04-01',2975,NULL,20);
INSERT INTO EMP VALUES (7654,'MARTIN','SALESMAN',7698,'81-09-10',1250,1400,30);
INSERT INTO EMP VALUES (7499,'ALLEN','SALESMAN',7698,'81-02-11',1600,300,30);
INSERT INTO EMP VALUES (7844,'TURNER','SALESMAN',7698,'81-08-21',1500,0,30);
INSERT INTO EMP VALUES (7900,'JAMES','CLERK',7698,'81-12-11',950,NULL,30);
INSERT INTO EMP VALUES (7521,'WARD','SALESMAN',7698,'81-02-23',1250,500,30);
INSERT INTO EMP VALUES (7902,'FORD','ANALYST',7566,'81-12-11',3000,NULL,20);
INSERT INTO EMP VALUES (7369,'SMITH','CLERK',7902,'80-12-11',800,NULL,20);
INSERT INTO EMP VALUES (7788,'SCOTT','ANALYST',7566,'82-12-22',3000,NULL,20);
INSERT INTO EMP VALUES (7876,'ADAMS','CLERK',7788,'83-01-15',1100,NULL,20);
INSERT INTO EMP VALUES (7934,'MILLER','CLERK',7782,'82-01-11',1300,NULL,10);

commit;

drop  table  salgrade;

create table salgrade
( grade   number(10),
  losal   number(10),
  hisal   number(10) );

insert into salgrade  values(1,700,1200);
insert into salgrade  values(2,1201,1400);
insert into salgrade  values(3,1401,2000);
insert into salgrade  values(4,2001,3000);
insert into salgrade  values(5,3001,9999);

commit;
```

### 조회

```sql
-- 사원번호를 찾아라
-- 사원번호를 입력하면 해당 사원의 급여가 나오도록 출력하세요!
-- 7782
ACCEPT p_empno prompt '사원 번호를 입력하세요 ~'
DECLARE
    v_sal number(10);
BEGIN
    SELECT SAL INTO v_sal
    FROM emp
    WHERE empno = &p_empno;
    
    DBMS_OUTPUT.PUT_LINE('월급은 '|| v_sal);
END;
```

실행) 7893

![Untitled](/images/PL_SQL_start/Untitled%206.png)

### 조건절

```sql
-- 조건절 & 반복문
-- 사원 이름을 입력합니다. 받는 급여가 고소득자인지, 중간 소득자, 저 소득자
-- KING, SCOTT
SELECT * FROM emp;

ACCEPT p_ename prompt '사원 이름을 입력하세요 ~ '
DECLARE 
    -- 변수 선언
    v_ename emp.ename%TYPE := upper('&p_ename');
    v_sal emp.sal%TYPE;
BEGIN
    SELECT sal into v_sal
    FROM emp
    WHERE ename = v_ename;
    DBMS_OUTPUT.PUT_LINE('급여 ' || v_sal);
    
    -- 조건식
    IF v_sal >= 3500 THEN 
        DBMS_OUTPUT.PUT_LINE('고 소득자');
    ELSIF v_sal >= 2000 THEN 
        DBMS_OUTPUT.PUT_LINE('중간 소득자');
    ELSE 
        DBMS_OUTPUT.PUT_LINE('저 소득자');
    END IF;
END;
```

실행) KING

![Untitled](/images/PL_SQL_start/Untitled%207.png)

### 반복문

- 구구단 예제

```sql
-- 반복문 
-- 구구단! 
2 x 1 = 2 = 2 x 1 
2 x 2 = 4 = 2 x 2
DECLARE 
    v_count number(10) := 0;
BEGIN 
    LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('2 x ' || v_count || ' = ' || 2 * v_count);
        EXIT WHEN v_count = 9;
    END LOOP;
END;
```

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술

[PL/SQL 실습01](https://www.notion.so/PL-SQL-01-fe33528bf2df49da993d17f993fea1ca)

[PL/SQL 실습02](https://www.notion.so/PL-SQL-02-60d75b5f672844c0a922e0e62a3abeb3)

[PL/SQL - ML](https://www.notion.so/PL-SQL-ML-e8d756adeecd41d38703208774006c44)