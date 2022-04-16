---
title: "WSL2 install"
tags:
  - wsl2
  - Notion
categories:
  - setting
  - wsl2
author: "minkuen"
date: '2022-04-14'
---

# WSL2 and Linux

다음 링크 참고 :

- 반드시 설정 확인
- [https://www.lainyzine.com/ko/article/how-to-install-wsl2-and-use-linux-on-windows-10/](https://www.lainyzine.com/ko/article/how-to-install-wsl2-and-use-linux-on-windows-10/)

Microsoft Store → windows terminal 설치 

→ windows powershell 관리자 권한으로 설치

→ [[Windows 10] WSL2 설치 및 사용법 - LainyZine](https://www.lainyzine.com/ko/article/how-to-install-wsl2-and-use-linux-on-windows-10/#google_vignette) 내용 참고하여 명령.

→ `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

→ `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

→ 재부팅

→ wsl2 Linux 커널 업데이트 패키지 설치 ( 위 링크 참고)

설치 실패 : ( This update only applies to machines with the windows subsystem for Linux)

       ㄴ [https://goaloflife.tistory.com/192](https://goaloflife.tistory.com/192) 로 해결해본다.

→ windows Terminal 

→ `wsl --set-default-version 2`

→ Microsoft Store → Ubuntu 설치

→ Ubuntu → 설치되기까지 기다린다

→ 이름 / 패스워드 입력 

( 이름 : kmk3593 / password : 2016***** )

→ windows terminal 

→ `wsl -l -v` 

→ Ubuntu Running 2 가 출력되면 성공.

### Linux Shell 프롬프트

windows terminal 

→ `wsl bash`

→ Bash 셸이 실행됨. 프롬프트 형태가 바뀌면 성공

## 저자 주:  여기서부터 WSL2 리눅스 셸 프롬프트

→ 즉, Windows 10 메인 디스크가 리눅스와 연결되어있으며,

 WSL2 Linux에서 Windows의 파일을 사용하는 것도 가능한 상태.

# setting 순서

- Nifi → Airflow → Elasticsearch → postgreSQL  → VSCord 순으로 세팅을 진행했다.

1. [Apache NiFi 설치와 설정 in WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/apache_nifi_wsl2/)
2. [Setting up Apache-Airflow in Windows using WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/apache_airflow_using_wsl2/)
3. [ElasticSearch & Kibana 설치 in WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/elasticsearch_kibana_wsl2/)
4. [PostgreSQL Installation on WSL2 and Windows - Data Science | DSChloe](https://dschloe.github.io/sql/postgreslq_wsl2/)
5. [VSCode Remote WLS 연동 - Data Science | DSChloe](https://dschloe.github.io/settings/vscode_wsl2/)