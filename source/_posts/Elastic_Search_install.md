---
title: "Elasticsearch Install"
tags:
  - setting
  - elasticsearch
  - kibana
categories:
  - setting
  - elasticsearch
author: "minkuen"
date: '2022-04-17'
---


## ****ElasticSearch & Kibana 설치 in WSL2****

[ElasticSearch & Kibana 설치 in WSL2 - Data Science | DSChloe](https://dschloe.github.io/settings/elasticsearch_kibana_wsl2/)

****Step 1. 사전 필수 패키지 설치****

0.우선 시스템 패키지를 업데이트 하고, HTTPS와 관련된 패키지를 설치한다.

Windows Terminal → wsl bash 

또는

Ubuntu → ..cd → ..cd

→`sudo apt-get update && sudo apt-get upgrade`

→ `sudo apt update`

→ `sudo apt install apt-transport-https`

1. 자바를 설치한다.
- 이미 설치가 되어 있다면 버전만 확인한다.

→ `sudo apt install openjdk-11-jdk`

→ `java -version`

2.  자바 환경 변수를 설정하기 위해 아래와 같이 에디터를 입력한다.

→ `sudo vi /etc/environment`

→ (그리고 다음내용을 추가한다.)

→ 인서트 모드에서 `JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"`

→ esc → :wq 하여 저장하고 나간다.

• 환경변수를 업데이트 한다.

• 그리고 실제 경로가 나오는지 확인한다.

→ `source /etc/environment`

→ `echo $JAVA_HOME`

→ /usr/lib/jvm/java-11-openjdk-amd64 가 출력되면 성공.

****Step 2. ElasticSearch 설치****

• GPG Keys를 확인하여 설치를 진행한다.

→ `wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -`

• 라이브러리를 아래와 같이 추가한다.

→ `sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list'`

• 이제 elasticsearch를 설치한다.

→ `sudo apt-get update`

→ `sudo apt-get install elasticsearch`

****Step 3. Elasticsearch 서비스 시작****

• 이번에는 elasticsearch 서비스를 시작한다.

→`sudo systemctl start elasticsearch`

에러 발생 :

System has not been booted with systemd as init system (PID 1). Can't operate.
Failed to connect to bus: Host is down

에러 해결 : 

 [boot - 시스템이 init system(PID 1)으로 systemd로 부팅되지 않았습니다. 작동 할 수 없음 - 우분투에게 물어보십시오. (askubuntu.com)](https://askubuntu.com/questions/1379425/system-has-not-been-booted-with-systemd-as-init-system-pid-1-cant-operate)

→ `sudo -b unshare --pid --fork --mount-proc /lib/systemd/systemd --system-unit=basic.target`

→ `sudo -E nsenter --all -t $(pgrep -xo systemd) runuser -P -l $USER -c "exec $SHELL"`

• 서비스가 가능하도록 한다.

• 그리고 서비스를 시작한다.

→ `sudo systemctl enable elasticsearch`

→ `sudo systemctl start elasticsearch`

• 실제 서비스가 작동하는지 확인한다.

→ `curl -X GET "localhost:9200/"`

→ 주소창에 입력 : localhost:9200/

→ windows Terminal과 같은 내용이 출력되면 성공

****Step 4. Kibana 설치 및 서비스 시작****

• 우선 kibana를 설치한다.

• 그리고 서비스를 활성화한다.

→ `sudo apt-get install kibana`

→ `sudo systemctl enable kibana`

• 서비스를 시작하고, 확인해본다

→ `sudo systemctl start kibana`

→ `sudo systemctl status kibana`

****Step 5. Kibana WebUI 확인****

• **[http://localhost:5601/](http://localhost:5601/)** 에서 확인해본다.

[Reference]

- Sayan Dey, ****How to install & uninstall Elasticsearch on Ubuntu 19.04, 18.04 & 16.04,**** **[https://www.how2shout.com/how-to/install-uninstall-elasticsearch-ubuntu-19-04-18-04-16-04.html](https://www.how2shout.com/how-to/install-uninstall-elasticsearch-ubuntu-19-04-18-04-16-04.html)**