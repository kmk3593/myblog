---
title: "Oracle_practice5"
tags:
  - oracle
categories:
  - SQL
  - oracle
author: "minkuen"
date: '2022-05-09'
---
# SQL 함수

### sql developer

- sql developer에서 새로운 sql 워크시트를 생성한다.
    
    도구 → sql워크시트 : ch04_0427
    
- 오라클 SQL과 PL/SQL을 다루는 기술

### ABS 함수

- 교재를 참고하여 코드를 익혀보자
- ABS 함수는 매개변수로 숫자를 받아 그 절대값을 반환하는 함수다.
- ABS는 다음과 같이 사용한다.

```sql
-- SQL 함수 살펴 보기
-- ABS

SELECT 
    ABS(10)
    , ABS(-10) 
    , ABS(10.123)
    , ABS(-10.123)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled.png)

### CEIL & FLOOR 함수

- **CEIL** 함수는 매개변수 n과 같거나 가장 큰 정수를 반환한다.
- **FLOOR** 함수는 CEIL 함수와는 반대로 매개변수 n보다 작거나 가장 큰 정수를 반환한다.

```sql
-- CELL & FLOOR
SELECT
    CEIL(10.123)
    , CEIL(-10.123)
    , FLOOR(10.123)
    , FLOOR(-10.213)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%201.png)

### ROUND 함수

- ****ROUND(n, i)****
- **ROUND** 함수는 매개변수 n을 소수점 기준 (i+1)번 째에서 반올림한 결과를 반환한다.
- i는 생략할 수 있고 디폴트 값은 0이다.
    - 즉 소수점 첫 번째 자리에서 반올림이 일어나 정수 부분의 일의 자리에 결과가 반영된다.

```sql
SELECT
    ROUND(10.154, 1)
    , ROUND(10.151, 2)
    , ROUND(-10.154, 1)
    , ROUND(-10.151, 2)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%202.png)

### TRUNC 함수

- ****TRUNC(n1, n2)****
- **TRUNC** 함수는 반올림을 하지 않고 n1을 소수점 기준 n2자리에서 잘라낸 결과를 반환한다.
- n2 역시 생략할 수 있으며 디폴트 값은 0이다.
- 양수일 때는 소수점 기준으로 오른쪽, 음수일 때는 소수점 기준 왼쪽 자리에서 잘라낸다.

```sql
-- TRUNC
-- 반올림 안함. 소수점 절삭
SELECT
    TRUNC(115.155)
    , TRUNC(115.155, 1)
    , TRUNC(115.155, 2)
    , TRUNC(115.155, -2)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%203.png)

### POWER & SQRT

- ****POWER(n2, n1)****
    - **POWER** 함수는 n2를 n1 제곱한 결과를 반환한다.
    - n1은 정수와 실수 모두 올 수 있는데, n2가 음수일 때 n1은 정수만 올 수 있다.
- ****SQRT(n)****
    - **SQRT** 함수는 n의 제곱근을 반환한다.

```sql
-- 128p
-- POWER(n2, n1) SQRT(n)
-- 제곱 & 제곱근
SELECT
    POWER(3, 2)
    , POWER(3, 3)
    , SQRT(9)
    , SQRT(8)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%204.png)

### MOD & REMAINDER

- ****MOD(n2, n1)****
    - **MOD** 함수는 n2를 n1으로 나눈 나머지 값을 반환한다.
- ****REMAINDER(n2, n1)****
    - **REMAINDER** 함수 역시 n2를 n1으로 나눈 나머지 값을 반환한다.
    - 나머지를 구하는 내부적 연산 방법이 MOD 함수와는 약간 다르다.

```sql
-- MOD(n2, n1)와 REMAINDER(n2, n1)
-- MOD 함수는 n2를 n1으로 나눈 나머지 값 반환
SELECT
    MOD(19,4)
    , REMAINDER(19,4)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%205.png)

### EXP, LN, LOG

- ****EXP(n)****
    - **EXP**는 지수 함수로 e(e=2.71828183…)의 n제곱 값을 반환한다.
- ****LN(n)****
    - **LN** 함수는 자연 로그 함수로 밑수가 e인 로그 함수다.
- ****LOG(n2, n1)****
    - **LOG**는 n2를 밑수로 하는 n1의 로그 값을 반환한다.

```sql
-- EXP, LN, LOG
SELECT EXP(2), LN(2.713), LOG(10,100)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%206.png)

### 문자 함수

### CONCAT

- ****CONCAT(char1, char2)****
- **CONCAT**함수는 ‘||’ 연산자처럼 매개변수로 들어오는 두 문자를 붙여 반환한다.

```sql
-- 문자 함수
-- CONCAT :  '||' 연산자처럼 두 문자를 붙여 반환
SELECT
    CONCAT('I Have', ' A Dream'),
    'I Have' || ' A Dream'
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%207.png)

### *SUBSTR*

- 주로 쓰이는 중요한 함수이다.
- ****SUBSTR(char, pos, len)****
- 잘라올 대사 문자열인 char의 pos번째 문자부터 len길이만큼 잘라낸 결과를 반환하는 함수다.
- pos 값으로 0이 오면 디폴트 값인 1, 즉 첫 번째 문자를 가리키며, 음수가 오면 char 문자열 맨 끝에서 시작한 상대적 위치를 의미한다.
- 또한 len 값이 생략되면 pos번째 문자부터 나머지 모든 문자를 반환한다.

```sql
-- SUBSTR (**** 중요함 ****)
-- 문자 개수 단위로 문자열 자름
SELECT 
    SUBSTR('ABCDEFG', 1, 4)
    , SUBSTR('ABCDEFG', -3, 4)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%208.png)

### SUBSTRB

- ****SUBSTRB(char, pos, len)****
- 문자열의 바이트 수만큼 출력한다.
- **SUBSTRB**는 문자 개수가 아닌 문자열의 바이트(BYTE) 수만큼 잘라낸 결과를 반환한다
- 나머지 처리 로직은 SUBSTR과 같다.

```sql
-- SUBSTRB
-- 문자열의 바이트 수만큼
SELECT 
    SUBSTRB('ABCDEFG', 1, 4)
    , SUBSTRB('가나다라마바사', 1, 4)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%209.png)

### LTRIM, RTRIM

- ****LTRIM(char, set),****
    - LTRIM 함수는 매개변수로 들어온 char 문자열에서 set으로 지정된 문자열을 왼쪽 끝에서 제거한 후 나머지 문자열을 반환한다.
    - 두 번째 매개변수인 set은 생략할 수 있으며, 디폴트로 공백 문자 한 글자가 사용된다.
- ****RTRIM(char, set)****
    - **RTRIM** 함수는 LTRIM 함수와 반대로 오른쪽 끝에서 제거한 뒤 나머지 문자열을 반환한다.

```sql
-- LTRIM(char, set), RTRIM(char, set)
SELECT
    LTRIM('ABCDEFGABC', 'ABC')
    , LTRIM('가나다라', '가')
    , RTRIM('ABCDEFGABC', 'ABC')
    , RTRIM('가나다라', '라')
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2010.png)

### LPAD, RPAD

- ****LPAD(expr1, n, expr2)****
    - **LPAD** 함수는 매개변수로 들어온 expr2 문자열(생략할 때 디폴트는 공백 한 문자)을 n자리만큼 왼쪽부터 채워 expr1을 반환하는 함수다.
    - 매개변수 n은 expr2와 expr1이 합쳐져 반환되는 총 자릿수를 의미한다.
    - 예를 들어, 서울의 지역 전화번호는 ‘02’인데 전화번호 컬럼에 지역번호가 없으면 LPAD 함수로 번호 02를 자동으로 채워 넣을 수 있다.
- ****RPAD(expr1, n, expr2)****
    - **RPAD**는 LPAD와는 반대로 오른쪽에 해당 문자열을 채워 반환한다.

```sql
-- LPAD, RPAD
-- 무언가를 입력해준다.
CREATE TABLE ex4_1 (
    phone_num VARCHAR2(30)
);

INSERT INTO ex4_1 VALUES('111-1111');
INSERT INTO ex4_1 VALUES('222-2222');
INSERT INTO ex4_1 VALUES('333-3333');

SELECT * FROM ex4_1;

-- (02)를 덧붙인다.
SELECT LPAD(phone_num, 12, '(02)') FROM ex4_1;
SELECT RPAD(phone_num, 12, '(02)') FROM ex4_1;
```

![Untitled](/images/Oracle_practice_5/Untitled%2011.png)

### 날짜 함수

- 날짜 함수는 DATE 함수나 TIMESTAMP 함수와 같은 날짜형을 대상으로 연산을 수행해 결과를 반환하는 함수다.

### ****SYSDATE, SYSTIMESTAMP****

- **SYSDATE와 SYSTIMESTAMP**는 현재 일자와 시간을 각각 DATE, TIMESTAMP 형으로 반환한다.

```sql
SELECT 
    SYSDATE
    , SYSTIMESTAMP
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2012.png)

### ADD_MONTHS

- ****ADD_MONTHS (date, integer)****
- ADD_MONTHS 함수는 매개변수로 들어온 날짜에 interger 만큼의 월을 더한 날짜를 반환한다.

```sql
-- ADD_MONTHS
SELECT
    ADD_MONTHS(SYSDATE, 1)
    , ADD_MONTHS(SYSDATE, -1)
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2013.png)

### MONTHS_BETWEEN

- ****MONTHS_BETWEEN(date1, date2)****
- **MONTHS_BETWEEN** 함수는 두 날짜 사이의 개월 수를 반환한다.
    - date2가 date1보다 빠른 날짜가 온다.

```sql
-- MONTHS_BETWEEN
SELECT
    MONTHS_BETWEEN(SYSDATE, ADD_MONTHS(SYSDATE, 1)) mon1
    , MONTHS_BETWEEN(ADD_MONTHS(SYSDATE, 1), SYSDATE) mon2
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2014.png)

### LAST_DAY

- ****LAST_DAY(date)****
- LAST_DAY는 date 날짜를 기준으로 해당 월의 마지막 일자를 반환한다.

```sql
-- LAST_DAY
-- 해당 달의 마지막 날
SELECT 
    LAST_DAY(SYSDATE)
    , LAST_DAY(ADD_MONTHS(SYSDATE, 1))
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2015.png)

### ROUND & TRUNC

- ROUND와 TRUNC는 숫자 함수이면서 날짜 함수로도 쓰인다.
- ****ROUND(date, format)****
    - ROUND는 format에 따라 반올림한 날짜를 반환한다.
- ****TRUNC(date, format)****
    - TRUNC는 잘라낸 날짜를 반환한다.

```sql
-- ROUND(date, format)
-- TRUNC(date, format)
SELECT 
    SYSDATE
    , ROUND(SYSDATE, 'month')
    , TRUNC(SYSDATE, 'month')
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2016.png)

### NEXT_DAY

- ****NEXT_DAY (date, char)****
- **NEXT_DAY**는 date를 char에 명시한 날짜로 다음 주 주중 일자를 반환한다.

```sql
-- NEXT_DAY (date, char)
SELECT NEXT_DAY(SYSDATE, '금요일')
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2017.png)

### TO_CHAR

- **TO_CHAR (숫자 혹은 날짜, format)**
- 숫자나 날짜를 문자로 변환해 주는 함수가 바로 TO_CHAR로, 매개변수로는 숫자나 날짜가 올 수 있고 반환 결과를 특정 형식에 맞게 출력할 수 있다.

```sql
-- 140p
-- 형변환 
SELECT TO_CHAR(123456789, '999,999,999')
FROM DUAL;

SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD')
FROM DUAL;
```

- 123456789를 문자로 변환

![Untitled](/images/Oracle_practice_5/Untitled%2018.png)

- 날짜 함수를 이용해 당일 날짜를 출력

![Untitled](/images/Oracle_practice_5/Untitled%2019.png)

- 매개변수로 오는 숫자나 날짜에 따라 자주 사용하는 포맷을 정리하면 다음과 같다.

![Untitled](/images/Oracle_practice_5/Untitled%2020.png)

![Untitled](/images/Oracle_practice_5/Untitled%2021.png)

### TO_NUMBER

- **TO_NUMBER(expr, format)**
- 문자나 다른 유형의 숫자를 NUMBER 형으로 변환하는 함수다.

```sql
-- TO_NUMBER(expr, format)
-- 문자나 다른 유형의 숫자를 NUMBER 형으로 변환하는 함수
SELECT TO_NUMBER('123456')
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2022.png)

### TO_DATE, TO_TIMESTAMP

- ****TO_DATE(char, format)****
    - 문자를 날짜형으로 변환하는 함수다.
    - **TO_DATE**는 DATE 형으로 변환해 값을 반환한다.

![Untitled](/images/Oracle_practice_5/Untitled%2023.png)

- ****TO_TIMESTAMP(char, format)****
    - 문자를 날짜형으로 변환하는 함수다.
    - **TO_TIMESTAMP**는 TIMESTAMP 형으로 변환해 값을 반환한다.

```sql
SELECT TO_DATE('20220427 14:07:20', 'YYYY-MM-DD HH24:MI:SS')
FROM DUAL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2024.png)

### NULL

- NULL을 비교할 때는 IS NULL이나 IS NOT NULL 구문을 사용하였다
- 오라클에서는 NULL을 연산 대상으로 처리하는 SQL 함수를 제공하고 있다

```sql
-- NULL 관련 함수
SELECT 
    NVL(manager_id, employee_id)
FROM employees
WHERE manager_id IS NULL;
```

![Untitled](/images/Oracle_practice_5/Untitled%2025.png)

### NLV

- ****NVL(expr1, expr2)****
- **NVL**함수는 expr1이 NULL일 때 expr2를 반환한다.

### NLV2

- ****NVL2((expr1, expr2, expr3)****
- **NVL2**는 NVL을 확장한 함수로 expr1이 NULL이 아니면 expr2를,

     NULL이면 expr3를 반환하는 함수다.

```sql
-- NVL2(expr1, expr2, expr3)
-- expr1이 NULL이 아니면 expr2 실행하라
-- expr1이 NULL이면 expr3을 실행하라
DESC employees;
SELECT
    employee_id
    , NVL2(commission_pct
        , salary + (salary + commission_pct)
        , salary) as final_salary
FROM employees;
```

![Untitled](/images/Oracle_practice_5/Untitled%2026.png)

### COALESCE

- ****COALESCE (expr1, expr2, …)****
- **COALESCE**는 매개변수로 들어오는 표현식에서 NULL이 아닌 첫 번째 표현식을 반환하는 함수다.

```sql
-- COALESCE(expr1, expr2, ...)
-- 매개변수로 들어오는 표현식에서 NULL이 아닌 첫번째 표현식 반환
SELECT
    employee_id
    , salary
    , commission_pct
    , COALESCE(salary * commission_pct, salary) AS salary2
FROM employees;
```

![Untitled](/images/Oracle_practice_5/Untitled%2027.png)

### LNNVL

- ****LNNVL(조건식)****
- **LNNVL**은 매개변수로 들어오는 조건식의 결과가 **FALSE나 UNKNOWN**
이면 **TRUE를, TRUE**이면 **FALSE**를 반환한다.

```sql
SELECT 
    -- count(*) -- 행 갯수 반환
    employee_id
    , commission_pct
FROM employees
WHERE LNNVL(commission_pct >= 0.2);
```

![Untitled](/images/Oracle_practice_5/Untitled%2028.png)

### NULLIF

- **NULLIF (expr1, expr2)**
- **NULLIF** 함수는 expr1과 expr2을 비교해 같으면 NULL을, 같지 않으면 expr1을 반환한다.

```sql
-- NULLIF
SELECT
    employee_id
    , TO_CHAR(start_date, 'YYYY') start_year
    , TO_CHAR(end_date, 'YYYY') end_year
    , NULLIF(TO_CHAR(end_date, 'YYYY'), TO_CHAR(start_date, 'YYYY'))
FROM job_history;
```

![Untitled](/images/Oracle_practice_5/Untitled%2029.png)

### DECODE

- ****DECODE (expr, search1, result1, search2, result2, …, default)****
- **DECODE**는 expr과 search1을 비교해 두 값이 같으면 result1을, 같지 않으면 다시 search2와 비교해 값이 같으면 result2를 반환하고, 이런 식으로 계속 비교한 뒤 최종적으로 같은 값이 없으면 default 값을 반환한다.

```sql
-- DECODE (IF-ELIF-ELIF-ELIF-ELSE)
SELECT UNIQUE(channel_id) FROM sales;

SELECT 
    prod_id
    , channel_id
    , DECODE(channel_id, 3, 'Direct', 
                         9, 'Direct', 
                         5, 'Indirect', 
                         4, 'Indirect', 
                            'Others') decodes
FROM sales
WHERE prod_id = 125;
```

![Untitled](/images/Oracle_practice_5/Untitled%2030.png)

- Reference : 오라클 SQL과 PL/SQL을 다루는 기술