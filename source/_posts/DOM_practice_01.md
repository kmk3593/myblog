---
title: "JavaScript DOM"
tags:
  - javascript
categories:
  - frontEnd 
  - javascript
author: "minkuen"
date: '2022-06-22'
---


### DOM 모델

- DOM : Document Object Model
- 문서내의 Node는 객체이고, 각 객체의 속성값을 통해 문서를 제어

![Untitled](/images/DOM_practice_01/Untitled.png)

### DOM 모델 실습 – img 모델 (1)

- img 속성값을 통해서 자바스크립트로 문서 변경하기

![Untitled](/images/DOM_practice_01/Untitled%201.png)

### 실습01

- 우선 이미지를 다운받아서 images 폴더에 넣어놓는다.
- 예시) images/img1.jpg

- 다운받은 이미지를 출력해보자
- 입력한 이미지를 새로 띄울 수 있도록 구현해보자

- dom_01.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>실습</title>
    <script src="dom_01.js"></script>
</head>
<body>
    <section id = "section1">
        <div>
            <input class = "src-input" type="text">
            <input class = "change-button" type="button" value="변경">
        </div>
        <div>
            <img class="img" src="images/img1.jpg">
        </div>
    </section>
</body>
</html>
```

- dom_01.js

```html
window.addEventListener("load", function(){

    let section = document.querySelector("#section1");
    let srcInput = section.querySelector(".src-input");
    let changeButton = section.querySelector(".change-button");
    let img = section.querySelector(".img");

    changeButton.onclick = function(){
        img.src = "images/" + srcInput.value;
    }    
});
```

- 지정한 경로의 이미지가 출력되었다

![Untitled](/images/DOM_practice_01/Untitled%202.png)

- 출력할 이미지의 경로를 입력하면 다음과 같이 변경된다
- 예시) img1.jpg

![Untitled](/images/DOM_practice_01/Untitled%203.png)

### 실습02

- 텍스트를 직접 입력하지 않아도 이미지를 바꿀 수 있게 해보자
- dom_02.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>실습</title>
    <script src="dom_02.js"></script>
</head>
<body>
    <section id = "section1">
        <div>
            <input class = "src-input" type="text">
            <select class = "img-select">
                <option value="img1.jpg">img1</option>
                <option value="img2.jpeg">img2</option>
                <option value="img3.jpg">img3</option>
            </select>
            <input class = "change-button" type="button" value="변경">
        </div>
        <div>
            <img class="img" src="images/img3.jpg">
        </div>
    </section>
</body>
</html>
```

- dom_02.js

```html
window.addEventListener("load", function(){

    let section = document.querySelector("#section1");
    // let srcInput = section.querySelector(".src-input");
    let imgSelector = section.querySelector(".img-select")
    let changeButton = section.querySelector(".change-button");
    let img = section.querySelector(".img");

    changeButton.onclick = function(){
        img.src = "images/" + imgSelector.value;
    } 
});
```

- 이미지 이름을 선택하고 변경할 수 있게 되었다.

![Untitled](/images/DOM_practice_01/Untitled%204.png)

### 실습03

- 이미지에 테두리 색을 입혀보자
- 테두리 색을 변경가능하게 작성한다
- dom_04.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>dom실습</title>
    <script src="dom_04.js"></script>
</head>
<body>
    <section id = "section1">
        <div>
            <input class="src-input" type="text" list="img-list">
            <datalist id="img-list">
                <option value="img1.jpg">img1</option>
                <option value="img2.jpg">img2</option>
                <option value="img3.jpg">img3</option>               
            </datalist>
            <input class="color-input" type="color">
            <input class="change-button" type="button" value="변경">
        </div>
        <div>
            <br>
            <img class="img" src="images/img1.jpg" style="border-width:5px; border-style:solid; border-color:red;">
        </div>
    </section>
</body>
</html>
```

- dom_04.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section1");
    let srcInput = section.querySelector (".src-input");
    // let imgSelector = section.querySelector(".img-select");
    let changeButton = section.querySelector(".change-button");
    let img = section.querySelector(".img");
    let colorInput = section.querySelector(".color-input");

    changeButton.onclick = function(){
        img.src = "images/" + srcInput.value;
        // img.style["border-color"] = colorInput.value;
        img.style.borderColor = colorInput.value;
    }
});
```

- 결과
- 테두리를 변경 가능하게 구현되었다.

![Untitled](/images/DOM_practice_01/Untitled%205.png)

### 실습04

- 리스트에 내용을 추가/삭제하는 기능을 만들어보자
- dom_5.html 일부

```html
<body>
    <section id = "section1">
        <div>
            <input class="title-input" type="text" name="title">
            <input class="add-button" type="button" value="추가">
            <input class="del-button" type="button" value="삭제">
        </div>
        <div class="menu-list">
            <li>HTML</li>
            <li>CSS</li>
            <li>JAVASCRIPT</li>
            <!-- <li>휴먼</li>  ==> 신규 생성됨.-->

        </div>
    </section>
</body>
```

- dom_05.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section1");
    let titleInput = section.querySelector(".title-input");
    let addButton = section.querySelector(".add-button");
    let delButton = section.querySelector(".del-button");
    let menuList = section.querySelector(".menu-list");
    
    addButton.onclick = function(){
        let textNode = document.createTextNode(titleInput.value);
        let liNode = document.createElement("li"); //li 태그를 만듦

        liNode.appendChild(textNode);   //li 태그에 textNode를 추가
        menuList.appendChild(liNode);   // menuList에 li 태그 추가
    };
    delButton.onclick = function(){
        let liNode = menuList.children[0]; // 자식중 첫번째 태그
        menuList.removeChild(liNode);   // li 태그를 부모에서 연결 제거
    };
});
```

- 결과

![Untitled](/images/DOM_practice_01/Untitled%206.png)

### 실습 05

- 테이블을 만들고 복사,입력, 템플릿 기능을 구현해보자
- dom_06.html 일부

```html
<body>
    <section id = "section1">
        <template>
            <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </template>
        <div>
            <input class="clone-button" type="button" value="복사">
            <input class="input-button" type="button" value="입력">
            <input class="temp-button" type="button" value="템플릿">
        </div>
        <table border="1" class="notice-list">
            <thead>
                <tr>
                    <td>번호</td>
                    <td>제목</td>
                    <td>내용</td>
                    <td>작성자</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>1</td>
                    <td>가입신청1</td>
                    <td>가입신청합니다.1</td>
                    <td>강*준</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>가입신청2</td>
                    <td>가입신청합니다.2</td>
                    <td>강*우</td>
                </tr>        
            </tbody>
        </table>
    </section>
</body>
```

- dom_06.js

```html
window.addEventListener("load", function(){
    let notices = [
    {"id":5, "title":"가입인사3", "content":"가입인사3", "writer":"강*혁"}
    ,{"id":6, "title":"가입인사4", "content":"가입인사4", "writer":"강*혁"}];
    let section = document.querySelector("#section1");
    let cloneButton = section.querySelector(".clone-button");
    let inputButton = section.querySelector(".input-button");
    let tempButton = section.querySelector(".temp-button");
    let noticeList = section.querySelector(".notice-list");

    tempButton.onclick = function(){
        let tempNode = section.querySelector("template");
        console.log(tempNode);
        // true는 하위 전체를 import함.
        let cloneNode = document.importNode(tempNode.content, true);
        let tds = cloneNode.querySelectorAll("td");
        tds[0].textContent = notices[0].id;
        tds[1].textContent = notices[0].title;
        tds[2].textContent = notices[0].content;
        tds[3].textContent = notices[0].writer;
        // tbodyNode 하위로 cloneNode를 붙여넣음.
        let tbodyNode = noticeList.querySelector("tbody");
        tbodyNode.appendChild(cloneNode);
    };    
    inputButton.onclick = function() {
        let tbodyNode = noticeList.querySelector("tbody");
        let trNode = noticeList.querySelector("tbody tr");
        // cloneNode는 trNode와 같은 형태.
        let cloneNode = trNode.cloneNode(true);
        // querySelectorAll로 인해서 td[0]~td[4]
        let tds = cloneNode.querySelectorAll("td");
        // td의 값을 notice의 값으로 바꿔치기 함.
        tds[0].textContent = notices[0].id;
        tds[1].textContent = notices[0].title;
        tds[2].textContent = notices[0].content;
        tds[3].textContent = notices[0].writer;
        // tbodyNode 하위로 cloneNode를 붙여넣음.
        tbodyNode.appendChild(cloneNode);
    };
    cloneButton.onclick = function(){
        let tbodyNode = noticeList.querySelector("tbody");
        // querySelector (먼저 있는 것 1개) 
        // querySelectorAll (모든 것을 배열로 가져옵니다.)
        let trNode = noticeList.querySelector("tbody tr");
        console.log(trNode);
        let cloneNode = trNode.cloneNode(true); 
        // true : tr하위까지 포함 복제하여 엘리먼트 생성
        // false : tr본인만 복제하여 엘리먼트 생성
        console.log(cloneNode);
        tbodyNode.appendChild(cloneNode);
        // tbody 엘리먼트 하위로 복제된 것을 연결함.
    };
});
```

- 결과
- 빈 상태에서 템플릿을 누르면 행 하나가 입력된다
- 입력하면 미리 설정한 행이 삽입된다
- 복사를 누르면 행 하나가 복사된다

![Untitled](/images/DOM_practice_01/Untitled%207.png)

### 실습06

- 행이 테이블 내에서 위,아래로 이동할 수 있게 해보자
- 위로 이동 버튼, 아래로 이동 버튼 구현
- dom_07.html 일부

```html
<body>
    <section id = "section1">
        <div>
            <input class="up-button" type="button" value="위로">
            <input class="down-button" type="button" value="아래로">
        </div>
        <table border="1" class="notice-list">
            <thead>
                <tr>
                    <td>번호</td>
                    <td>제목</td>
                    <td>내용</td>
                    <td>작성자</td>
                </tr>
            </thead>
            <tbody>
                <tr style="background-color: lightblue;">
                    <td>1</td>
                    <td>가입신청1</td>
                    <td>가입신청합니다.1</td>
                    <td>강*준</td>
                </tr>
                <tr>
                    <td>2</td>
                    <td>가입신청2</td>
                    <td>가입신청합니다.2</td>
                    <td>강*우</td>
                </tr>        
                <tr>
                    <td>3</td>
                    <td>가입신청3</td>
                    <td>가입신청합니다.3</td>
                    <td>강*혁</td>
                </tr>  
            </tbody>
        </table>
    </section>
</body>
```

- dom_07.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section1");
    let upButton = section.querySelector(".up-button");
    let downButton = section.querySelector(".down-button");
    let tbodyNode = section.querySelector("tbody");
    
    let currentNode = tbodyNode.firstElementChild;

    downButton.onclick = function(){
        let nextNode = currentNode.nextElementSibling;
        if(nextNode == null) {
            alert ("더 이상 이동불가합니다.");
            return;
        }
        // insertBefore란, currentNode 앞으로 nextNode를 이동한다. 
        tbodyNode.insertBefore(nextNode, currentNode);
    };    
    upButton.onclick = function() {
        let prevNode = currentNode.previousElementSibling;
        if(prevNode == null) {
            alert ("더 이상 이동불가합니다.");
            return;
        }
        // insertBefore란, prevNode 앞으로 currentNode 이동한다. 
        tbodyNode.insertBefore(currentNode, prevNode);
    };
});
```

- 결과
- 버튼을 눌렀을 때, 1번 행이 아래로 이동하는 것을 확인

![Untitled](/images/DOM_practice_01/Untitled%208.png)

### 실습07

- 체크박스를 사용한다
- 모두 체크하기, 체크한 행 삭제하기, 행 위치 교환 기능을 구현
- dom_08.html 일부

```html
<body>
    <section id = "section1">
        <div>
            <input class="del-button" type="button" value="일괄삭제">
            <input class="swap-button" type="button" value="선택노드 바꾸기">
        </div>
        <table border="1" class="notice-list">
            <thead>
                <tr>
                    <td><input type="checkbox" class="overall-checkbox"></td>
                    <td>번호</td>
                    <td>제목</td>
                    <td>내용</td>
                    <td>작성자</td>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><input type="checkbox" unchecked></td>
                    <td>1</td>
                    <td>가입신청1</td>
                    <td>가입신청합니다.1</td>
                    <td>강*준</td>
                </tr>
                <tr>
                    <td><input type="checkbox"></td>
                    <td>2</td>
                    <td>가입신청2</td>
                    <td>가입신청합니다.2</td>
                    <td>강*우</td>
                </tr>        
                <tr>
                    <td><input type="checkbox"></td>
                    <td>3</td>
                    <td>가입신청3</td>
                    <td>가입신청합니다.3</td>
                    <td>강*혁</td>
                </tr>  
            </tbody>
        </table>
    </section>
</body>
```

- dom_08.js

```html
window.addEventListener("load", function(){
    let section = document.querySelector("#section1");
    let delButton = section.querySelector(".del-button");
    let swapButton = section.querySelector(".swap-button");
    let tbodyNode = section.querySelector("tbody");
    let allcheckbox = section.querySelector(".overall-checkbox");

    delButton.onclick = function(){
        // 체크된 것만 inputs에 포함됨.
        // 체크가 안된 것 만 포함할 경우는 "input[type='checkbox']:unchecked
        let inputs = tbodyNode.querySelectorAll
                            ("input[type='checkbox']:checked");
        for (let i=0 ; i<inputs.length; i++) {
            //체크박스는 input 태그임. input==>TD==>TR. 이시점에서 remove
            inputs[i].parentElement.parentElement.remove();
        }
    };    
    swapButton.onclick = function(){
        // 체크된 것만 inputs에 포함됨.
        let inputs = tbodyNode.querySelectorAll
                ("input[type='checkbox']:checked");
        if (inputs.length !=2) {
            alert("2개만 체크해주세요");
            return;
        }
        trs=[];
        for(let i=0; i<inputs.length; i++) {
            // trs에 선택된 2개의 input==>td==>tr의 내용을 넣음
            trs.push(inputs[i].parentElement.parentElement);
        }
        // 첫번째것을 복사해서 clone으로 생성
        let cloneNode = trs[0].cloneNode(true);
        // 두번째것과 복제된 것을 교체 
        trs[1].replaceWith(cloneNode);
        // 첫번째 것과 두번째 것을 교체 
        trs[0].replaceWith(trs[1]);
    };
    allcheckbox.onclick = function(){
        let inputs = tbodyNode.querySelectorAll("input[type='checkbox']");
        for (let i=0 ; i<inputs.length; i++) {
            // allcheckbox의 체크 형태를 기준으로 각 체크박스에 대입함.
            inputs[i].checked = allcheckbox.checked;
        }
    };    

});
```

- 결과
- 모두 체크, 체크한 행 삭제, 행 위치 교환 모두 정상 작동을 확인

![Untitled](/images/DOM_practice_01/Untitled%209.png)