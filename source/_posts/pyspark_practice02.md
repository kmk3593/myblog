---
title: "pyspark 실습02"
tags:
  - spark
categories:
  - python
  - library
  - pyspark
author: "minkuen"
date: '2022-04-27'
---

**사전준비**

- git bash로 VSCord에 들어가 터미널을 연다.

바탕화면 우클릭 : git bash here

→ `cd pyspk_project`

→ `code .`

→ git bash 터미널

**pyspark 실습(1)**

- 가상환경 진입하고 파일 생성

→ `source venv/Scripts/activate`

→ chapter01_get_starged 폴더에서 파일 생성

→ 파일 생성 : step04_structype.py

키워드 : Struct Type

구글링 : Spark Struct Type, Spark Struct 

참고 링크 :  

[https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html)

→ 코드 작성

```python
from struct import Struct
from pyspark.sql import SparkSession
from pyspark.sql import functions as func 
from pyspark.sql.types import StructType, StructField, IntegerType, LongType

# 세션 할당 (필수)
# spark = SparkSession.builder.appName("")
spark = SparkSession.builder.appName("PopularMovies").getOrCreate()

# 스키마 작성 (u.logs 데이터)
schema = StructType(
    [
        StructField("userID", IntegerType(), True),
        StructField("movieID", IntegerType(), True),
        StructField("rating", IntegerType(), True),
        StructField("timestamp", LongType(), True)
    ]
) 

print("Schema is done")

# 데이터 불러오기
movies_df = spark.read.option("sep", "\t").schema(schema).csv("ml-100k/u.logs")

# 내림차순으로 인기있는 영화 정렬
# movieID 그룹바이. count() orderby
toMovieIds = movies_df.groupBy("movieID").count().orderBy(func.desc('count'))

print(movies_df.show(10))

# 세션 종료
spark.stop()
```

→ 경로 이동 : `cd chapter01_get_started`

→ 저장 후 실행

→ `python step04_structype.py`

→ 다음 테이블이 출력되어야 한다.

![Untitled](/images/pyspark_practice02/Untitled.png)

**pyspark 실습(2)**

→ chapter01_get_starged 폴더에서 파일 생성

→ 파일 생성 : step05_advancestructype.py

→ 코드 작성

```python
from pyspark.sql import SparkSession
from pyspark.sql import functions as func
from pyspark.sql.types import StructType, StructField, IntegerType, LongType
import codecs

print("Hello")

def loadMovieNames():
    movieNames = {}
    with codecs.open("ml-100k/u.ITEM", "r", encoding="ISO-8859-1", errors="ignore") as f:
        for line in f:
            fields = line.split("|")
            movieNames[int(fields[0])] = fields[1]
    return movieNames

# 세션 할당
spark = SparkSession.builder.appName("PopularMovies").getOrCreate()

# 파이썬 딕셔너리 객체를 Spark 객체로 변환
nameDict = spark.sparkContext.broadcast(loadMovieNames())

# 스키마 작성 (u.logs 데이터)
schema = StructType(
    [
        StructField("userID", IntegerType(), True)
        , StructField("movieID", IntegerType(), True)
        , StructField("rating", IntegerType(), True)
        , StructField("timestamp", LongType(), True)
    ]
)

print("Schema is done")

# 데이터 불러오기
movies_df = spark.read.option("sep", "\t").schema(schema).csv("ml-100k/u.logs")

# 내림차순으로 인기있는 영화 정렬
# movieID 그룹바이. count() orderby
topMovieIds = movies_df.groupBy("movieID").count()

# 딕셔너리
# key-value
# 키 값을 알면 value 자동으로 가져옴 (movieTitle)
def lookupName(movieID):
    return nameDict.value[movieID]

lookupNameUDF = func.udf(lookupName)

# MovieTitle 기존 topMovieIds 데이터에 추가
# 컬럼을 추가
moviesWithNames = topMovieIds.withColumn("movieTitle", lookupNameUDF(func.col("movieID")))

final_df = moviesWithNames.orderBy(func.desc("count"))

print(final_df.show(10))

# 세션 종료
spark.stop()
```

→ 저장 후 실행

→ `python step05_advancestructype.py`

→ 다음과 같이 출력된다.

![Untitled](/images/pyspark_practice02/Untitled%201.png)

- Reference : [https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html)