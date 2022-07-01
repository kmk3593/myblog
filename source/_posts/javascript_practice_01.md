---
title: "Java Script 실습01"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-16'
---


### Java Script란?

- 1단계 : HTML 문서란 document 객체로 변환하여 로딩
- 2단계 : document 객체 기반으로 화면에 보여짐
- 중간에서 JAVA Script는 이 객체의 정보에 접근하여 관리가 가능

![Untitled](/images/javascript_practice_01/Untitled.png)

### JAVA Script 탄생배경

![Untitled](/images/javascript_practice_01/Untitled%201.png)

### 데이터 - 값의 종류 및 변환

- const = 상수. 변하지 않는다
- 정수 = int
- 실수 = double
- 문자 = char
- 문자열 = string

![Untitled](/images/javascript_practice_01/Untitled%202.png)

### Java Script 사용해보기

- VSCord에서 다음 코드 작성
- <script> </script>를 이용한다

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        alert("휴먼교육센터");
        console.log("휴먼교육센터");
        document.write("후먼교육센터")
    </script>
</head>
<body>
    
</body>
</html>
```

- 해당 html 파일을 열어본다.
- 작성한 코드가 반영된다. 다른 코드도 같은 방식으로 진행하자

![Untitled](/images/javascript_practice_01/Untitled%203.png)

### 데이터 - 참조형 변수

![Untitled](/images/javascript_practice_01/Untitled%204.png)

### 데이터 - 배열변수

![Untitled](/images/javascript_practice_01/Untitled%205.png)

### 데이터 - 배열 변수 초기화

![Untitled](/images/javascript_practice_01/Untitled%206.png)

### 데이터 - list 관리

![Untitled](/images/javascript_practice_01/Untitled%207.png)

- splice 까지 실습한 코드이다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        let nums = new Array();
        nums.push(3);
        nums.push(13);
        nums.push(25);
        console.log(nums);  // 배열의 형태로 3,13,25
        
        let n1 = nums.pop(); // 가장 위에 있는 25 제거
        console.log("nums : ", nums);
        console.log("n1 : ", n1);

        let num2 = new Array(2,3,"hello", 7);
        console.log(num2);      // 배열
        console.log(num2[2]);   // "hello"
        let num3 = new Array(2, 3, "hello", 7, new Array(2,3,4));
        console.log(num3[4]);   // [2, 3, 4]
        console.log(num3[4][1]);    // 3

        num2.splice(2);         // 3~4번째가 삭제
        console.log(num2);
        num2.splice(2,1);       // 3번째에서 1개만 삭제 
        console.log(num2);
        num2.splice(2,1, "HUMAN");// 3번째에서 1개 삭제 후 HUMAN 삽입
        num2.splice(2,0, "COMP");
        // 3번째에서 0개 삭제 후 COMP 삽입
        

    </script>
</head>
<body>
</body>
</html>
```

- 해당 html의 console 창이다

![Untitled](/images/javascript_practice_01/Untitled%208.png)

### 데이터 - object 객체

![Untitled](/images/javascript_practice_01/Untitled%209.png)

- 객체에 관해 실습해보았다.

```html
   <script>
        var exam = {"kor":90, "eng":80, "math":70}
        console.log(exam);
        console.log(exam.kor + exam.math);
        // 자바 스크립트는 배열변수 내에 여러 타입을 담을 수 있다
        var ar = [3, 4, 5, 6, exam, [7,8,9]];

        console.log(ar[1]);     // 4
        console.log(ar[4]);     // {"kor":90, "eng":80, "math":70}
        console.log(ar[4][0]);  // undifined
        console.log(ar[4]["kor"]);  // 90
        console.log(ar[4].math);    // 70
        console.log(ar[5]);     // [7,8,9]
        console.log(ar[5][1]);  // 8
    </script>

```

- 결과는 다음과 같다

![Untitled](/images/javascript_practice_01/Untitled%2010.png)

![Untitled](/images/javascript_practice_01/Untitled%2011.png)

- Reference : Do it! 웹 사이트 따라 만들기
    - [http://www.easyspub.co.kr/30_Menu/DataList/PUB](http://www.easyspub.co.kr/30_Menu/DataList/PUB)