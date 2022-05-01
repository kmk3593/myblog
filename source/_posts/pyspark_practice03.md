---
title: "pyspark 실습03"
tags:
  - spark
categories:
  - python
  - library
  - pyspark
author: "minkuen"
date: '2022-04-28'
---

**사전준비**

- git bash로 VSCord에 들어가 터밀널을 연다.

바탕화면 우클릭 : git bash here

→ `cd pyspk_project`

→ `code .`

→ git bash 터미널

**pyspark 실습(1)**

- 가상환경 진입하고 폴더, 파일 생성

→ `source venv/Scripts/activate`

→ 폴더 생성 : chapter02_get_cleansing

- 슬랙에서 data.zip 을 다운로드
- 압축을 풀고 chapter02_get_cleansing 파일에 복사하여 옮긴다.

→ 파일 생성 : pipeline.py

![Untitled](/images/pyspark_practice03/Untitled.png)

- 코드를 작성해본다.

→ 코드 작성

`from pyspark.sql import SparkSession`

`from pyspark.sql.functions import *`

`print("Hello!")`

→ 저장

→ 경로 이동 : `cd chapter02_get_cleansing`

→ 실행 : `python pipeline.py`

- 이어서 코드작성

→ pipeline.py를 다음과 같이 작성

```
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql import functions as F

# print("Hello!!")

# 스파크 세션을 생성
spark = SparkSession.builder.master("local[1]").\
    appName("quickpipeline").getOrCreate()

# 데이터 불러오기
df = spark.read.csv("data\AA_DFW_2015_Departures_Short.csv.gz"
                    , header = True)

print("file loaded")

print(df.show())

# remove duration = 0
df = df.filter(df[3] > 0)

# ADD ID column
df = df.withColumn('id', F.monotonically_increasing_id())
df.show()

df.write.csv("data/output.csv", mode = "overwrite")

spark.stop()
```

→ 저장 후 실행

→ `python pipeline.py`

→ output.csv 가 생성되면 성공이다.

![Untitled](/images/pyspark_practice03/Untitled%201.png)

**pyspark 실습(2)**

- 온도를 측정하는 코드를 작성해본다.
- 슬랙에서 다운로드
    - 1800.csv, book.txt, customer-orders.csv, fakefriends.csv
- chapter02_get_cleansing/data 파일에 복사하여 옮긴다.

파일 생성 : min_temp.py

→ 코드 작성

`from pyspark import SparkConf, SparkContext`

`conf = SparkConf().setMaster('local').setAppName('MinTemperatures')`

`sc = SparkContext(conf = conf)`

`print("Hello")`

→ 저장 후 실행

→ `python min_temp.py`

- 이어서 코드작성

→ min_temp.py를 다음과 같이 작성

from pyspark import SparkConf, SparkContext

conf = SparkConf().setMaster('local').setAppName('MinTemperatures')

sc = SparkContext(conf = conf)

print("Begins...")

def parseLine(line):

fileds = line.split(',') # 문자열을 split

stationID = fileds[0]

entryType = fileds[2]

temperature = float(fileds[3]) * 0.1 * (9.0 / 5.0) + 32.0

return (stationID, entryType, temperature)

lines = sc.textFile('data/1800.csv')

#print(lines)

parseLines = lines.map(parseLine)

#print(parseLine)

minTemps = parseLine.filter(lambda x : "TMIN" in x[1])

stationTemps = minTemps.map(lambda x: (x[0], x[2]))

minTemps = stationTemps.map(lambda x, y: min(x,y))

results = minTemps.collect()

print(results)

→ 저장 후 실행

→ `python min_temp.py`

**pyspark 실습(3)**

- 나이를 출력하는 코드를 작성해보자

파일 생성 : friends-by-age.py

→ 코드 작성

```
from pyspark import SparkConf, SparkContext

conf = SparkConf().setMaster("local").setAppName("FriendsByAge")
sc = SparkContext(conf = conf)

def parseLine(line):
    fields = line.split(',')
    age = int(fields[2])
    numFriends = int(fields[3])
    return (age, numFriends)

lines = sc.textFile("logs/fakefriends.csv")
rdd = lines.map(parseLine)
totalsByAge = rdd.mapValues(lambda x: (x, 1)).reduceByKey(lambda x, y: (x[0] + y[0], x[1] + y[1]))
averagesByAge = totalsByAge.mapValues(lambda x: x[0] / x[1])
results = averagesByAge.collect()
for result in results:
    print(result)
```

→ 저장 후 실행

→ `python friends-by-age.py`

**pyspark 실습(4)**

파일 생성 : totalspent.py

→ 코드 작성

```
# 라이브러리 불러오기
from pyspark import SparkConf, SparkContext

# 사용자 정의 함수
def extractCusPrice(line):
    fields = line.split(",")
    return (int(fields[0]), float(fields[2]))

# main 함수
def main():

    # 스파크 설정
    conf = SparkConf().setMaster("local").setAppName('SpentbyCustomer')
    sc = SparkContext(conf = conf)

    # 데이터 불러오기
    input = sc.textFile("data/customer-orders.csv")
    # print("is data?")
    mappedInput = input.map(extractCusPrice)
    totalByCustomer = mappedInput.reduceByKey(lambda x, y : x + y)
		# 정렬
    filpped = totalByCustomer.map(lambda x: (x[1], x[0]))
    totalByCustomerStored = filpped.sortByKey()

    results = totalByCustomer.collect()
    for result in results:
        print(result)

# 실행 코드
if __name__ == "__main__":
    main()
```

→ 저장 후 실행

→ `python totalspent.py`

- Reference : [https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html](https://spark.apache.org/docs/latest/api/python/reference/api/pyspark.sql.types.StructType.html)