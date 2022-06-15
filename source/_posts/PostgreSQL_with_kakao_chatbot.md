title: "PostgreSQL_with_kakao_chatbot"
tags:
  - heroku
  - postgreSQL
categories:
  - chatbot
  - kakao_chatbot
author: "minkuen"
date: '2022-06-03'
---



## 챗봇 평점 남기기 기능 구현

- 평가 점수를 입력받아 DB에 기록하고 평균 통계를 계산한다.
- 단, 1사람당 1번씩 평점 남기기가 가능하며 2번 이상부터는 가장 최근 점수로 갱신된다.

- 알고리즘
    - id 검색 후, 없을 경우 평가를 기록 = INSERT
    - id 검색 후, 있을 경우 평가를 갱신 = UPDATE

- 코드 작성

```python
import psycopg2
from datetime import datetime

passwd =                '5280c3caeed8c1cb512f19d6fc238a6ab642556e69c3050ddfe232c4c4372d0e'
db = psycopg2.connect(host='ec2-3-234-131-8.compute-1.amazonaws.com', dbname='ec2-3-234-131-8.compute-1.amazonaws.com',user='ndurbfpbebgdrc',password= passwd,port=5432)
cur=db.cursor()

# 날짜, id, 점수 
date_data = datetime.today().strftime('%Y-%m-%d')
id_data = "'ww'"
idid_data = 'ww'
score_data = '2'

# SELECT문 - id로 검색하여 조회
cur.execute("SELECT * FROM score WHERE id=%s;" % (id_data))
rows = cur.fetchall()
print(rows)
print(type(rows))

# rows 길이 = 0 
# 해당 id가 남긴 기록이 없음 = 첫 평가
# 점수를 포함한 데이터를 INSERT
if len(rows) == 0:
    cur.execute("INSERT INTO score (date, id, score) VALUES (%s, %s, %s);"
            , (datetime.today().strftime('%Y-%m-%d'), idid_data, score_data) )

# rows 길이 != 0
# 해당 id가 남긴 기록이 있음 = 최소 두 번째 평가
# 기존에 남긴 점수를 새로 UPDATE
else :
    cur.execute("UPDATE score SET date=%s, score=%s WHERE id=%s;"
            , (datetime.today().strftime('%Y-%m-%d'),score_data, idid_data) )

# cur.execute("SELECT * FROM score WHERE id=%s;" % (id_data))
# rows = cur.fetchall()
# print(rows)
# print(type(rows))

# POSTGRESQL DB에 COMMIT 하기
# db.commit()
```

- 챗봇 스킬로 사용 가능하도록 형식을 맞추어 다시 작성

```python
# # db에 점수추가
@app.route('/api/dbinsert', methods=['POST'])
def dbinsert():
    body = request.get_json() # 사용자가 입력한 데이터

    # date_data = datetime.today().strftime('%Y-%m-%d')
    id_data = "'%s'" %str(body['userRequest']['user']['id'])
    idid_data = '%s' %str(body['userRequest']['user']['id'])
    score_data = str(list(body['userRequest']['utterance'])[1])
    cur=db.cursor()

    cur.execute("SELECT * FROM score WHERE id=%s;" % (id_data))
    rows = cur.fetchall()
    
    if len(rows) == 0:
        cur.execute("INSERT INTO score (date, id, score) VALUES (%s, %s, %s);"
                , (datetime.today().strftime('%Y-%m-%d'), idid_data, score_data) )

    else :
        cur.execute("UPDATE score SET date=%s, score=%s WHERE id=%s;"
                , (datetime.today().strftime('%Y-%m-%d'),score_data, idid_data) )

    db.commit()

    responseBody = {
        "version": "2.0",
        "template": {
            "outputs": [
                {
                    "simpleText": {
                        "text": "점수가 반영되었습니다.\n감사합니다."
                    }
                }
            ]
        }
    }

    return responseBody
```

- 블록 제작
- 별점 버튼을 점수 저장할 블록으로 연결

![Untitled](/images/PostgreSQL_with_kakao_chatbot/Untitled.png)

- 스킬 만들고 적용하기

![Untitled](/images/PostgreSQL_with_kakao_chatbot/Untitled%201.png)

- 실행 결과

![Untitled](/images/PostgreSQL_with_kakao_chatbot/Untitled%202.png)

![Untitled](/images/PostgreSQL_with_kakao_chatbot/Untitled%203.png)