---
title: "Spark on Windows"
tags:
  - spark
categories:
  - setting
  - spark
author: "minkuen"
date: '2022-04-25'
  

[Spark Installation on Windows 10 - Data Science | DSChloe](https://dschloe.github.io/python/python_edu/00_settings/spark_installation_windows_10/)

## 사전준비

- 스파크를 설치하는 과정이다.
- 사전에 파이썬 3가 설치되어 있어야 한다.
- 만약, 파이썬이 처음이라면 **[Anaconda](https://www.anaconda.com/products/individual)**를 설치한다.

## **자바 다운로드**

- 자바를 설치한다. 설치 파일은 아래에서 다운로드 받는다.
    - 설치파일: **[Java SE 8 Archive Downloads (JDK 8u211 and later)](https://www.oracle.com/java/technologies/javase/javase8u211-later-archive-downloads.html)**
- 설치 시, 오라클 로그인이 필요 할 수도 있다.

## S**park 다운로드**

- 이번에는 Spark를 설치한다.
- **설치파일 다운로드**
    - 설치 URL: **[https://www.apache.org/dyn/closer.lua/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz](https://www.apache.org/dyn/closer.lua/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz)** (2022년 1월 기준)

![Untitled](/images/Spark_on_Windows/Untitled.png)

### **WinRAR 다운로드**

- 이 때, `.tgz` 압축파일을 풀기 위해서는 `WinRAR` 을 설치한다.
    - 설치 파일: **[https://www.rarlab.com/download.htm](https://www.rarlab.com/download.htm)**
    - 본인 컴퓨터에 맞는 것을 설치한다.
    - WinRARx64 (64bit) 6.11 버전 다운로드

![Untitled](/images/Spark_on_Windows/Untitled%201.png)

## **winutils 다운로드**

- 이번에는 스파크가 윈도우 로컬 컴퓨터가 Hadoop으로 착각하게 만들 프로그램이 필요하다.
    - 설치파일: **[https://github.com/cdarlint/winutils](https://github.com/cdarlint/winutils)**
    - 여기에서 각 설치 버전에 맞는 winutils를 다운로드 받는다.
- 이전에 받은 spark-3.2.0-bin-hadoob-3.2.tgz 와 버전이  일치하는 것을 선택해야 한다.
    - 3.2.0 버전을 다운로드 받았다.

![Untitled](/images/Spark_on_Windows/Untitled%202.png)

## **자바 설치 진행**

- C 드라이브에 폴더 생성 : hadoob
- 다운로드 받은 파일 4개를 C/hadoob 에 복사하여 옮긴다

![Untitled](/images/Spark_on_Windows/Untitled%203.png)

- 관리자 권한으로 실행 : jdk-8u311-windows-x64

![Untitled](/images/Spark_on_Windows/Untitled%204.png)

- 계속 Next 버튼 클릭 후, 아래 파일에서 경로를 수정한다. (이 때, `Program Files` 공백이 있는데, 이러한 공백은 환경 설치 시 문제가 될 수 있다.)
- Development Tools 선택
- change 버튼으로 변경을 진행한다.

![Untitled](/images/Spark_on_Windows/Untitled%205.png)

- c 드라이브 경로로 이동
- Foldername: jdk 입력
    - 다음 그림과 같아야 한다.

![Untitled](/images/Spark_on_Windows/Untitled%206.png)

- Java를 다른 폴더에 설치하려 한다.
- 변경(C)...

![Untitled](/images/Spark_on_Windows/Untitled%207.png)

- c 드라이브 경로에서 ‘새 폴더 만들기(M)’
- 폴더 생성 : jre

![Untitled](/images/Spark_on_Windows/Untitled%208.png)

- 다음과 같이 설치 위치가 지정된다.

![Untitled](/images/Spark_on_Windows/Untitled%209.png)

- 성공적으로 설치되었다.

![Untitled](/images/Spark_on_Windows/Untitled%2010.png)

### **winrar 설치 진행**

- 관리자 권한으로 실행 : winrar-x64-611

![Untitled](/images/Spark_on_Windows/Untitled%2011.png)

- 기본 설정으로 설치 진행

![Untitled](/images/Spark_on_Windows/Untitled%2012.png)

## **spark 설치 진행**

- Spark 설치를 진행한다.
- 설치 파일 우클릭 → Extract to “spark-3.2.0-bin-hadoop3.2|”

![Untitled](/images/Spark_on_Windows/Untitled%2013.png)

### **spark 폴더 생성 및 파일 이동**

- 위 과정 이후 폴더가 생성된다.
- 파일 이동을 하도록 한다.
    - spark-3.2.0-bin-hadoop3.2 폴더 내 모든 파일을 복사한다.
- 그 후, C드라이브 하단에 spark 폴더를 생성한 후, 모두 옮긴다.

![Untitled](/images/Spark_on_Windows/Untitled%2014.png)

### **log4j.properties 파일 수정**

- `C` -> `spark` → `conf` → `[log4j.properties](http://log4j.properties)` 파일을 연다.
- 해당 파일을 메모장으로 연 후, 아래에서 `INFO` → `ERROR` 로 변경한다.
    - 작업 실행 시, 출력하는 모든 logs 값들을 없앨 수 있다.
    - 다음과 같이 설정 후 저장

![Untitled](/images/Spark_on_Windows/Untitled%2015.png)

## **winutils 설치 진행**

- C드라이브에서 winutils-bin 폴더를 차례로 생성한다.
- 다운로드 받은 winutils 파일을 복사하여 옮긴다.

![Untitled](/images/Spark_on_Windows/Untitled%2016.png)

- 이 파일이 Spark 실행 시, 오류 없이 실행될 수 있도록 파일 사용 권한을 얻도록 한다.
    - 이 때에는 CMD 관리자 권한으로 파일을 열어서 실행한다.
- 관리자 권한으로 실행 : 명령 프롬프트

![Untitled](/images/Spark_on_Windows/Untitled%2017.png)

- 다음 코드들을 시행

→ `cd c:\winutils\bin`

→ `winutils.exe chmod 777 \tmp\hive`

- 만약, ChangeFileModeByMask error (3) 에러 발생 시,
    
    C드라이브 하단에, `tmp\hive` 폴더를 차례대로 생성을 한다.
    

![Untitled](/images/Spark_on_Windows/Untitled%2018.png)

- 실행 결과, 에러가 발생했으므로 C드라이브에 폴더를 생성한다.
- 폴더 생성 : tmp
    - 폴더 생성 : hive
- 다시 코드를 실행한다.

→ `winutils.exe chmod 777 \tmp\hive`

→ 오류없이 실행되었다.

![Untitled](/images/Spark_on_Windows/Untitled%2019.png)

## **환경변수 설정**

- ‘시스템 환경 변수 편집’ 열기

→ `환경 변수(N)..` 

![Untitled](/images/Spark_on_Windows/Untitled%2020.png)

시스템 환경변수를 설정한다.

- 각 사용자 계정에 `사용자 변수 - 새로 만들기 버튼`을 클릭한다.

![Untitled](/images/Spark_on_Windows/Untitled%2021.png)

- 다음과 같이 설정
- `SPARK_HOME` 환경변수를 설정한다.

![Untitled](/images/Spark_on_Windows/Untitled%2022.png)

- `JAVA_HOME` 환경변수를 설정한다.

![Untitled](/images/Spark_on_Windows/Untitled%2023.png)

- `HADOOP_HOME` 환경변수를 설정한다.

![Untitled](/images/Spark_on_Windows/Untitled%2024.png)

- 환경변수를 편집한다.
- Path 선택 → 편집(E)...

![Untitled](/images/Spark_on_Windows/Untitled%2025.png)

- 아래 코드를 추가한다.
- 새로 만들기
    - `%SPARK_HOME%\bin`
    - `%JAVA_HOME%\bin`

![Untitled](/images/Spark_on_Windows/Untitled%2026.png)

## **파이썬 환경설정**

- Python 환경설정을 추가한다.
- `PYSPARK_PYTHON` 환경변수를 설정한다.

![Untitled](/images/Spark_on_Windows/Untitled%2027.png)

- `PYSPARK_DRIVER_PYTHON` 환경변수를 설정한다.
- 일단 지운다.

![Untitled](/images/Spark_on_Windows/Untitled%2028.png)

- `PYSPARK_DRIVER_PYTHON_OPTS` 환경변수를 설정한다.
- 일단 삭제한다.

![Untitled](/images/Spark_on_Windows/Untitled%2029.png)

## **스파크 테스트**

- 명령  프롬프트에서 진행

→ `c:\spark` 폴더로 경로를 설정 한다.

→ `pyspark`

![Untitled](/images/Spark_on_Windows/Untitled%2030.png)

- 이번에는 `[README.md](http://README.md)` 파일을 불러와서 아래 코드가 실행되는지 확인한다.
- 다음 코드를 실행해 본다.

→`rd = sc.textFile("README.md")`

→`rd.count()`

→ 다음 결과 출력 시 성공.

![Untitled](/images/Spark_on_Windows/Untitled%2031.png)

- Reference
    - [Spark Installation on Windows 10 - Data Science | DSChloe](https://dschloe.github.io/python/python_edu/00_settings/spark_installation_windows_10/)

[pyspark 실습_1](https://www.notion.so/pyspark-_1-118d1109403e451e9f5b2f5a81627a7e)

[pyspark_실습_2](https://www.notion.so/pyspark_-_2-4213c5f5b33f48c6b0156526d2023dc0)

[pyspark_실습_3](https://www.notion.so/pyspark_-_3-8bf9e94aab3942b0ae4759d21b236878)

[Spark on linux](https://www.notion.so/Spark-on-linux-0c14b4d491af46d787230fd974e9dde4)

[Spark UI](https://www.notion.so/Spark-UI-f2e00f267df64d16af47be23678d2c09)

[Spark ML](https://www.notion.so/Spark-ML-017307a2900a4d028ad32817f42d400a)