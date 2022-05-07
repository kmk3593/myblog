---
title: "Oracle_setting"
tags:
  - oracle
categories:
  - setting
  - oracle
author: "minkuen"
date: '2022-05-04'
---

## 사전준비

- 오라클을 설치한다.

구글링 : oracle database 19c download

[Oracle Database 19c Download for Microsoft Windows x64 (64-bit) | Oracle 대한민국](https://www.oracle.com/kr/database/technologies/oracle19c-windows-downloads.html)

![Untitled](/images/Oracle_setting/Untitled.png)

- SQL Developer 설치한다.

구글링 : sql developer

[Oracle SQL Developer Downloads](https://www.oracle.com/tools/downloads/sqldev-downloads.html)

![Untitled](/images/Oracle_setting/Untitled%201.png)

- c 드라이브  경로에 폴더 생성 : sql_lecture

앞서 다운로드한 설치 파일을 sql_lecture 폴더에 정리한다.

- 압축 해제한다.

우클릭 후에 “extract WINDOWS.X64\”

- 관리자 권한으로 실행 : setup
- 다음 경로로 이동하여 실행하면 된다.

c 드라이브 → sql_lecture 폴더 → WINDOWS.X64_193000_db_home 폴더 → setup

![Untitled](/images/Oracle_setting/Untitled%202.png)

- 체크 : 단일 인스턴스 데이터베이스 생성 및 구성

![Untitled](/images/Oracle_setting/Untitled%203.png)

- 체크 : 데스크톱 클래스

![Untitled](/images/Oracle_setting/Untitled%204.png)

- 체크 : 가상 계정 사용

![Untitled](/images/Oracle_setting/Untitled%205.png)

- 오라클 SQL과 PL/SQL을 다루는 기술 22p 참고하여 설정한다.
- 전역 데이터베이스 이름 : myoracle
- 비밀번호 : 1234
- 체크 해제 : 컨테이너 베이스로 생성

![Untitled](/images/Oracle_setting/Untitled%206.png)

- 설치까지 진행한다.
- 설치 완료

![Untitled](/images/Oracle_setting/Untitled%207.png)

## **1단계 sqlplus 실행하기**

- 관리자 권한으로 실행  : SQL Plus

![Untitled](/images/Oracle_setting/Untitled%208.png)

- 정보를 입력한다.

→사용자명 : `system`

→비밀번호 : `1234`

![Untitled](/images/Oracle_setting/Untitled%209.png)

## **2단계 : 테이블 스페이스 생성하기**

- 오라클 SQL과 PL/SQL을 다루는 기술  27p 참고
- 다음 코드를 사용하여 테이블 스페이스를 생성한다.
    - 테이블 스페이스는 myts라 명명하고 100MB 크기로 생성
    - 만약 데이터가 증가하면 5MB씩 자동 증가 옵션 추가

→`CREATE TABLESPACE myts DATAFILE 'C:\sql_lecture\oradata\MYORACLE\myts.dbf' SIZE 100M AUTOEXTEND ON NEXT 5M;`

![Untitled](/images/Oracle_setting/Untitled%2010.png)

## **3단계 : 사용자 생성**

- 해당 사용자에게 롤(Role, 권한)을 부여해야 한다. 현 시점에서는 ‘ora_user’ 사용자에게 DBA라는 롤을 부여한다.
    - 이 권한을 부여받으면 오라클에서 제공하는 웬만한 기능을 모두 사용한다.
    
- 사용자를 생성하는 코드를 작성한다.

(패스워드를 evan으로 할 경우, 다음과 같이 작성)

→`CREATE USER ora_user IDENTIFIED BY evan DEFAULT TABLESPACE MYTS TEMPORARY TABLESPACE TEMP;`

![Untitled](/images/Oracle_setting/Untitled%2011.png)

## **4단계 : 사용자 계정으로 DB에 접속하기**

- ora_user로 접속한다.

→`GRANT DBA TO ora_user;`

→`connect ora_user/evan;`

- 접속 후, show user; 입력하면 현재 로그인한 사용자 이름이 출력된다.

→  `show user;`

![Untitled](/images/Oracle_setting/Untitled%2012.png)

## **SQL Developer 실행**

- 새 접속 화면이 나타나면 접속 이름, 사용자 이름을 ora_user로 입력, 비밀번호는 입력, SID 항목에는 처음 설치 시 이름인 myoracle을 입력하고 테스트를 실행한다.

- 압축 해제한다.

우클릭 후에 “extract sqldeveloper214.3...”

- 관리자 권한으로 실행 : sqldeveloper
- 다음 경로로 이동하여 실행하면 된다.

c 드라이브 → sql_lecture 폴더 → sqldeveloper-21.4.3.063.0100-x64 폴더

→ sqldeveloper 폴더 → sqldeveloper

- 만약 다음 확인 창이 출력되면 ‘아니오’ 선택한다.

![Untitled](/images/Oracle_setting/Untitled%2013.png)

- Oracle 접속을 새로 만든다.

우클릭 : Oracle 접속 → 새 접속

![Untitled](/images/Oracle_setting/Untitled%2014.png)

- 다음과 같이 설정하고 ‘테스트’
    - 사용자 이름 : ora_user
    - 비밀번호 : evan
- 상태 : 성공
- 성공했다면 ‘접속’

![Untitled](/images/Oracle_setting/Untitled%2015.png)

- 다음과 같이 출력된다.

![Untitled](/images/Oracle_setting/Untitled%2016.png)

### 환경설정

- 다음 환결설정에서 인코딩을 UTF-8로 변경한다.
    - 메뉴 바 → 도구 → 환경 설정 → 환경 → 인코딩 : UTF-8

![Untitled](/images/Oracle_setting/Untitled%2017.png)

## **SQL Developer 날짜 기록**

- 다음 경로로 [NLS] 항목을 선택한다.
    - 메뉴 바 → 도구 → 환경 설정 → 데이터 베이스 → NLS
- NLS에서 ‘시간 기록 형식’을 수정.
    - 다음과 같이 수정한다.
    - 시간 기록 형식 : `YYYY/MM/DD HH24:MI:SS`

![Untitled](/images/Oracle_setting/Untitled%2018.png)

## **샘플 스키마 설치**

- expall.dmp와 expcust.dmp 파일을 내려 받는다.
    - URL : **[https://github.com/gilbutITbook/006696/tree/master/01장 환경설정](https://github.com/gilbutITbook/006696/tree/master/01%EC%9E%A5%20%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95)**
- c 드라이브에 폴더 생성
    - 폴더 생성 : backup
- backup 폴더에 expall.dmp와 expcust.dmp 파일을 옮긴다.

![Untitled](/images/Oracle_setting/Untitled%2019.png)

- 관리자 권한으로 실행 : 명령 프롬프트
- C:\backup 경로로 이동한다.
- 다음 코드 실행 : expall.dmp 을 올린다.

→ `imp ora_user/evan file=expall.dmp log=empall.log ignore=y grants=y rows=y indexes=y full=y`

- 다음 코드 실행 : expcust.dmp 을 올린다.

→ `imp ora_user/evan file=expcust.dmp log=expcust.log ignore=y grants=y rows=y indexes=y full=y`

![Untitled](/images/Oracle_setting/Untitled%2020.png)

- 임포트가 정상 종료되었다면 Oracle SQL로 이동하여 작업
- 다음 코드를 작성

→ `SELECT table_name FROM user_tables;`

→ 실행 : ctrl + enter

→ 다음과 같이 출력되면 성공.

![Untitled](/images/Oracle_setting/Untitled%2021.png)

- Git 연동

[SQL Developer with Git - Data Science | DSChloe](https://dschloe.github.io/sql/sql_developer_git/)

- Reference
    - [오라클 19c 기본 세팅 - Data Science | DSChloe](https://dschloe.github.io/sql/oracle_basic_settings/)
    - 오라클 SQL과 PL/SQL을 다루는 기술
    

[Oracle 실습01](https://www.notion.so/Oracle-01-258c74449f7a4702ac7467e8a6b0f625)

[Oracle 실습02](https://www.notion.so/Oracle-02-636623398364433b83a639c7d38180d4)

[Oracle 실습03](https://www.notion.so/Oracle-03-87b53c73e8de435784c75d42ccbe2ea3)

[Oracle 실습04](https://www.notion.so/Oracle-04-9d7e412bb0a04a3bbcdf4f51c2bd8a3d)

[Oracle 실습05](https://www.notion.so/Oracle-05-d2556785ba544df08bffc522d8a091a3)

[Oracle 실습06](https://www.notion.so/Oracle-06-e6d9ef003103443599879907fc62cedd)

[Oracle on Jupyter Lab](https://www.notion.so/Oracle-on-Jupyter-Lab-309b8ea23af042dea205e8664c8c6387)