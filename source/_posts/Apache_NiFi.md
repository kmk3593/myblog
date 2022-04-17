---
title: "Apache Nifi Install"
tags:
  - setting
  - NiFi
categories:
  - setting
  - NiFi
author: "minkuen"
date: '2022-04-15'
---

# Apache NiFi

[Apache NiFi 설치와 설정 in WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/apache_nifi_wsl2/)

## **설치**

- wsl2에서 JAVA 설치 한다.

관리자 권한으로 실행 : Ubuntu

→ `ls`  → `cd ..` → `ls` → `cd ..` → `ls`  // ls 하여 파일 출력 될 때까지

→ `java --version`

→ 설치 안 되어 있을 시 : `sudo apt-get update && sudo apt-get upgrade`

→ 설치 안 되어 있을 시 : `sudo apt install openjdk-11-jdk`

→ `vi ~/.bash_profile`

→ vi 편집기로 이동된다.

→ 내용 추가 : `export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64`

→ esc + :wq 하여 저장

- source 사용하여 상태 저장

→ `source ~/.bash_profile`

→ `echo $JAVA_HOME`

→ 다음 내용 출력 시 성공 : /usr/lib/jvm/java-11-openjdk-amd64  

- curl을 이용해서 NiFi를 현재 경로에 내려받는다. 오래 걸린다.

→ `sudo wget https://downloads.apache.org/nifi/1.16.0/nifi-1.16.0-bin.tar.gz`

→ `ls` 

→ 현재 있는 기본 경로에 nifi 가 출력 됨을 알 수 있다.

![Untitled](/images/Apache_NiFi/Untitled.png)

- /mnt/c 경로로 파일을 옮기자.
- mv 명령이 안 먹혀서 cp 명령 사용
- 다음 명령을 실행하여 /mnt/c 경로로 복사 붙여넣었다.
- 참고 자료 : [리눅스 / 명령어 / cp / 복사하는 명령어, mv – 이동하는 명령어 – MANUAL FACTORY](https://www.manualfactory.net/10805)

→`cp nifi-1.16.0-bin.tar.gz mnt/c/nifi-1.16.0-bin.tar.gz`

→ `cd mnt`

→ `cd c`

→ `ls`

→ /mnt/c 경로에 nifi 가 생겼다.

![Untitled](/images/Apache_NiFi/Untitled%201.png)

- .tar.gz 파일의 압축을 푼다

→ `sudo tar xvaf nifi` 까지 타이핑하고 Tab 하여 다음 코드 작성

→ `sudo tar xvzf nifi-1.16.0-bin.tar.gz`

- 압축파일을 푼 다음에는 cd nifi-1.16.0 폴더에 접속을 한다.

→ Tab 이용하여 다음 코드 작성하고 실행

→ `cd nifi-1.16.0/bin`

- ls를 실행해서 **[nifi-env.sh](http://nifi-env.sh/)** 파일이 있는지 확인하고 있다면, vi 에디터로 연다.
- bash_profile에서 한 것처럼 동일하게 자바 환경변수를 잡아준다

→ `sudo vi nifi-env.sh`

→ 내용 추가 : `export JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"`

→ esc + :wq 하여 저장하고 나온다.

- 그리고, **[nifi-env.sh](http://nifi-env.sh/)** 파일을 실행

→ `sudo ./nifi.sh start`

- NiFi 화면에 접속한다. **[https://127.0.0.1:8443/nifi/login](https://127.0.0.1:8443/nifi/login)**

→ 몇 분간 새로고침한다. ( 계속 안될 경우 : stop하고 기록을 지운 다음 다시 start)

→ 비공개 화면 ... 이라는 문구가 출력된다.

→ ‘고급’ 선택

→ 나타나는 주소를 클릭하여 들어간다.

→ 다음 화면이 출력된다.

![Untitled](/images/Apache_NiFi/Untitled%202.png)

- 종료

/mnt/c/nifi-1.16.0$ 상태에서 다음 명령 실행해야 한다.

→ `cd ..`

→ `sudo ./bin/nifi.sh stop`

- 로그인 준비.
- 아이디와 비밀번호를 설정한다. ( *비밀번호는 최소 13자리)

→ `sudo ./bin/nifi.sh set-single-user-credentials human 1234567890123`

- 그리고, **[nifi-env.sh](http://nifi-env.sh/)** 파일을 실행
- 단, /bin 경로에서 한다.

→ `cd bin/`

→ `sudo ./nifi.sh start`

- NiFi 화면에 접속한다. **[https://127.0.0.1:8443/nifi/login](https://127.0.0.1:8443/nifi/login)**

→ 몇 분간 새로고침한다.

→ 다음 정보로 로그인

id : human

password : 1234567890123

→ 다음 화면이 출력되면 성공.

![Untitled](/images/Apache_NiFi/Untitled%203.png)

- 세팅은 끝났으니 일단 종료시켜놓자.
- 종료
- /mnt/c/nifi-1.16.0$ 상태에서 다음 명령 실행해야 한다.

→ `cd ..`

→ `sudo ./bin/nifi.sh stop`

### 기록 지우는 법

ubuntu에서 다음 명령 실행

`cd..`

`cd..`

`cd mnt/c`

`ls`

`cd nifi-1/16/0/`

`ls`

`cd logs`

`ls`

`sudo rm -rf *`

`ls`

→ 삭제 되어 아무것도 출력되지 않는다.

### NiFi 사용법

- Nifi 사용법을 익혀보자
- 실무 예제로 배우는 데이터 공학 19p 부터 따라해본다.

메뉴바에서 process를 드래그하여 캔버스에 놓는다.

→ 다음 그림의 우측 상단에서 검색한다.

→ 검색 : GenerateFlowFile

→ ADD 버튼 클릭

![Untitled](/images/Apache_NiFi/Untitled%204.png)

→ 같은 방법으로 검색

→ 검색 : putfile

→ ADD

나타난 박스를 우클릭 → configure

→ properties

→ field 를 설정할 수 있다.

설정 후에는 박스끼리 연결할 수 있다.

→ 박스 하나의 중앙을 드래그하여 다른 박스에 놓는다.

→ 연결된다.

→ 이 상태에서 GenerateFlowFile에서 파일을 생성하여 PutFile에 옮길 수 있다.

![Untitled](/images/Apache_NiFi/Untitled%205.png)

- Reference : 실무 예제로 배우는 데이터 공학