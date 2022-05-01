---
title: "Spark on Linux"
tags:
  - spark
categories:
  - setting
  - spark
author: "minkuen"
date: '2022-04-29'
---


[WSL2에서의 Spark 설치 - Data Science | DSChloe](https://dschloe.github.io/settings/spark_install_using_wsl/)

## **개요**

- 간단하게 PySpark를 설치해보는 과정을 작성한다.
- WSL2 설치 방법은 다루지 않는다.

## **필수 파일 설치**

- 설치가 안 되었을 경우에 설치한다.
- 자바 및 Spark 파일을 설치하도록 한다.

```
$ sudo apt-get install openjdk-8-jdk
$ sudo wget https://archive.apache.org/dist/spark/spark-3.2.0/spark-3.2.0-bin-hadoop3.2.tgz
$ sudo tar -xvzf spark-3.2.0-bin-hadoop3.2.tgz
```

## **.bashrc 파일 수정**

- 경로를 다음과 같이 설정한다.

```
evan@evan:/mnt/c/hadoop$ pwd
/mnt/c/hadoop
```

- 설치한 파일은 다음과 같다.

```
evan@evan:/mnt/c/hadoop$ ls
spark-3.2.0-bin-hadoop3.2  spark-3.2.0-bin-hadoop3.2.tgz
```

- `vi ~/.bashrc` 파일을 열고 다음과 같이 코드를 작성한다.
    - 다른 코드는 건드리지 않는다.
    - 마지막 라인에서 작성한다.

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export SPARK_HOME=/mnt/c/spark
export PATH=$JAVA_HOME/bin:$PATH
export PATH=$SPARK_HOME/bin:$PATH
export PYSPARK_PYTHON=/usr/bin/python3
```

![Untitled](/images/Spark_on_linux/Untitled.png)

## **테스트**

- pyspark를 실행한다. (경로에 주의한다)
- SPARK_HOME을 다음과 같이 설정했으니 해당 경로에서 실행.
- export SPARK_HOME=/mnt/c/spark

경로 이동 : `cd ..` 

→ `cd spark/`

→`source ~/.bashrc`

→`pyspark`

![Untitled](/images/Spark_on_linux/Untitled%201.png)

- 정상적으로 작동한지 테스트한다.
- 해당 경로에 [README.md](http://README.md) 파일이 있다면 시행해보자.

→`rd = sc.textFile("README.md")`

→`rd.count()`

→ 다음과 같이 출력된다면 성공이다.

![Untitled](/images/Spark_on_linux/Untitled%202.png)

- Reference : [WSL2에서의 Spark 설치 - Data Science | DSChloe](https://dschloe.github.io/settings/spark_install_using_wsl/)