---
title: "JavaScript Event"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-24'
---

### 이벤트 객체

- Keyboard 및 Mouse 등의 입력장치에서는 이벤트가 발생함
- 발생한 Event의 속성값들을 대상으로 문서의 변경을 활용할 수 있음

![Untitled](/images/javaScript_event/Untitled.png)

### 이벤트 관리

- 이벤트는 Window라는 객체가 모든 객체를 대상으로 관리하고 있음.
- 최하단의 객체의 이벤트는, 상위로 이벤트를 발생시키고 있음. (상위 객체에서 관리 가능함)

![Untitled](/images/javaScript_event/Untitled%201.png)

### 이벤트 객체의 메서드(1)

- EVENT 인터페이스가 최상단이며, UI > 키보드, 마우스(휠 포함) Event 인터페이스가 있음

![Untitled](/images/javaScript_event/Untitled%202.png)

### 이벤트 객체의 메서드(2)

- EVENT 인터페이스가 최상단이며, UI > 키보드, 마우스(휠 포함) Event 인터페이스가 있음
- Mouse는 X,Y의 좌표를 확인할 수 있도록 인터페이스 제공함

![Untitled](/images/javaScript_event/Untitled%203.png)

### 이벤트 객체의 메서드(3)

- EVENT 인터페이스가 최상단이며, UI > 키보드, 마우스(휠 포함) Event 인터페이스가 있음
- Keyboard는 눌려진 Key 및 ALT/SHIFT 등을 확인할 수 있도록 인터페이스 제공함

![Untitled](/images/javaScript_event/Untitled%204.png)

### 마우스 이벤트 실습

- 마우스 이벤트는 e.target이란 객체로 속성값들을 사용할 수 있음

![Untitled](/images/javaScript_event/Untitled%205.png)

- event_01.html 일부

```html
<body>
    <section id = "section">
        <!-- 세번째 방법으로 bubbling 효과를 확인 -->
        <div id ="img-list">
            <img class="img" src="images/img1.jpg">
            <img class="img" src="images/img2.jpg">
            <img class="img" src="images/img3.jpg">
            <input type="text">
        </div>
        <div>
            <img class="current-img" src="images/img1.jpg">
        </div>
    </section>
</body>
```

- event_01.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section");
    let imgList = section.querySelector("#img-list");
    let imgs = section.querySelectorAll(".img");
    let currentImg = section.querySelector(".current-img");

    /*  첫번째 방법 : 이미지들 중 클릭된 것만 대상으로 src 변경하여 이미지 변경
    imgs[0].onclick = function(e) {
        currentImg.src = e.target.src;
    }
    imgs[1].onclick = function(e) {
        currentImg.src = e.target.src;
    }
    imgs[2].onclick = function(e) {
        currentImg.src = e.target.src;
    }
    */

    /*  두번째 방법 : 첫번째 방법을 for문을 활용하여 코드 간결화
    for (let i=0 ; imgs.length ; i++) {
        imgs[i].onclick = function(e) {
            currentImg.src = e.target.src;
        }
    }
    */

    // 세번째 방법 : 상위 객체에서도 이벤트를 bubbling을 통해서 받기 때문에.
    //              상위 객체에서도 관리가 가능합니다. 
    //              다만, img가 아닌 것은 제외하면서 이미지의 경로를 변경 작업함.
    imgList.onclick = function(e) {
        console.log(e.target.className);
        if (e.target.className != 'img') {
            return; 
        }
        currentImg.src = e.target.src;
    }

});
```

- 결과
- 클릭한 이미지가 아랫 열에 출력되도록 구현되었다

![Untitled](/images/javaScript_event/Untitled%206.png)

### 마우스 이벤트 실습 - trigger

- 특정 Element 이벤트는 다른 Element 이벤트를 호출할 수 있음 (트리거)
- Span tag의 클릭이 file 선택하는 input Tag를 클릭하게 함.

![Untitled](/images/javaScript_event/Untitled%207.png)

- trigger_01.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>event</title>
    <style>
        .file-button{
            /* 버튼은 숨김. */
            display:none;
        }
        .file-trigger-button {
            background-color: green;
            border : 1px solid lightgreen;
            border-radius: 5px;
            /* 상하는 5px, 좌우는 10px */
            padding : 5px 10px;
            color : white;
            /* 버튼 위로 마우스가 올라가면 클릭을 유도하는 포인터 */
            cursor : pointer;
        }
        .file-trigger-button:hover {
            background-color: lightgreen;
        }
    </style>
    <script src="trigger_01.js"></script>
</head>
<body>
    <section id="section">
        <input type="file" class="file-button">
        <span class="file-trigger-button">파일선택</span>
    </section>
</body>
</html>
```

- trigger_01.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section");
    let fileButton = section.querySelector(".file-button");
    let fileTriggerButton = section.querySelector(".file-trigger-button");

    // fileButton.onclick에 대해서는 미정의
    fileButton.onclick = function(e) {
    };
    fileTriggerButton.onclick = function(e) {
        let event = new MouseEvent("click", {
            'view':window,
            'bubbles' : true,
            'cancelable' : true
        })
        // 숨겨진 fileButton은 event(위에서 정의한 마우스이벤트)를 수행한다.
        fileButton.dispatchEvent(event);
    }
});
```

- 결과
- 파일 선택 후 의도한 결과가 출력되었다

![Untitled](/images/javaScript_event/Untitled%208.png)

### 마우스 이벤트 실습 - X,Y 좌표 이용

- 마우스 이벤트 발생시 X,Y 좌표를 활용할 수 있음
- X,Y 좌표는 여러가지의 형태로 존재함.

![Untitled](/images/javaScript_event/Untitled%209.png)

- 사각형을 만든다
- 클릭한 곳으로 사각형이 이동하도록 작성해보자
- event_02.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>event 실습</title>
    <style>
				body{
            margin : 0px 0px;
        }
        .container{
            width: 800px;
            height: 400px;
            border: 1px solid gray;
        }
        .box{
            width: 100px;
            height: 100px;
            border: 1px solid blue;
            background: blue;
        }
    </style>
    <script src="event_02.js"></script>
</head>
<body>
    <section id = "section">
        <div class = "container">
            <div class="box"></div>
        </div>
    </section>
</body>
</html>
```

- event_02.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section");
    let container = section.querySelector(".container");
    let box = section.querySelector(".box");

    container.onclick = function(e){
        console.log("(x,y) = " + e.x, e.y);
        console.log("(client) = " + e.clientX, e.clientY);
        console.log("(page) = " + e.pageX, e.pageY);
        console.log("(offset) = " + e.offsetX, e.offsetY);

        box.style.position = "absolute";
        box.style.left = e.x + "px";
        box.style.top = e.y + "px";
    }
});
```

- 결과
- 클릭한 위치로 사각형이 이동한다

![Untitled](/images/javaScript_event/Untitled%2010.png)

- 이번에는 사각형을 드래그하여 움직히에 한다
- event_02.js에 다음 코드를 추가한다.

```html
let offset = {x:0, y:0};

// on mounse down = 마우스가 눌린 상태
container.onmousedown = function(e){
    // 석택된 객체가 box라면, dragging을 true로 처리
    if(e.target == box){
        dragging = true;
    }
};

// 마우스가 떨어진 상태
container.onmouseup = function(e){
    // 선택된 객체가 box라면 dragging을 false로 처리
    if(e.target == box){
        dragging = false;
    }
};

box.onmousedown = function(e){
    offset.x = e.offsetX;
    offset.y = e.offsetY;
}
```

- 캡쳐로는 차이가 없지만 클릭 후에만 이동하게 구현되었다

![Untitled](/images/javaScript_event/Untitled%2011.png)