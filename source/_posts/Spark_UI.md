---
title: "Spark UI"
tags:
  - spark
categories:
  - setting
  - spark
author: "minkuen"
date: '2022-04-30'
---

- 가상환경을 생성한다.

/mnt/c 경로에서 실행

→`mkdir temp`

→`cd temp`

→`virtualenv venv`

![Untitled](/images/Spark_UI/Untitled.png)

- 가상환경에서 pyspark를 설치한다.

→ `source venv/bin/activate`

→ `pip install pyspark`

- 다음 링크 접속

[Quick Start - Spark 3.2.1 Documentation (apache.org)](https://spark.apache.org/docs/latest/quick-start.html)

- 다음 내용을 복사한다.

![Untitled](/images/Spark_UI/Untitled%201.png)

- [README.md](http://READ.md) 파일 내용이다.

```
This program just counts the number of lines containing 'a' and the number containing 'b' in a text file. Note that you'll need to replace YOUR_SPARK_HOME with the location where Spark is installed. As with the Scala and Java examples, we use a SparkSession to create Datasets. For applications that use custom classes or third-party libraries, we can also add code dependencies to spark-submit through its --py-files argument by packaging them into a .zip file (see spark-submit --help for details). SimpleApp is simple enough that we do not need to specify any code dependencies.

We can run this application using the bin/spark-submit script:
```

→`mkdir data`

→`cd data`

→`ls`

→`vi README.md`

→ 위에서 복사한 내용을 붙여넣는다.

→ `:wq`

→ 내용 확인`cat README.md`

→ `cd ..`

→ `vi SimpleApp.py`

→ 코드 작성

```
from pyspark.sql import SparkSession

logFile = "data/README.md"  # Should be some file on your system
spark = SparkSession.builder.appName("SimpleApp").getOrCreate()
logData = spark.read.text(logFile).cache()

numAs = logData.filter(logData.value.contains('a')).count()
numBs = logData.filter(logData.value.contains('b')).count()

print("Lines with a: %i, lines with b: %i" % (numAs, numBs))

input("Typing....")

spark.stop()
```

→ 저장 후 실행

→ python3 SimpleApp.py

→ 경로 확인 : `echo $SPARK_HOME`

→ `$SPARK_HOME/bin/spark-submit --master local[4] SimpleApp.py`

![Untitled](/images/Spark_UI/Untitled%202.png)

- 코드 샐행 후
- 위 결과 참고하여 address 복사

→ 뒤에 :4041을 추가하여 주소창에 입력한다. 

(코드 실행 후 나오는 텍스트에서 SparkUI를 확인하자)

→ 주소창에 입력하여 접속 : [http://172.19.91.118:4041](http://172.19.91.118:4041/)

→ 다음 화면 출력 시 성공.

![Untitled](/images/Spark_UI/Untitled%203.png)

- Reference :
    - [Quick Start - Spark 3.2.1 Documentation](https://spark.apache.org/docs/latest/quick-start.html)
    - [(apache.org)](https://spark.apache.org/docs/latest/quick-start.html)[https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html)