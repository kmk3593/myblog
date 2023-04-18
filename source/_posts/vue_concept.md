---
title: "Vue.js 기초 개념"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-04-18'
---


[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****

### Vue는 무엇인가?

- View = HTML. 브라우저에서 사용자에게 보여지는 요소들  (버튼, 입력 창 등)
- DOM = HTML 은 DOM을 이용해 JAVA Script로  조작할 수 있게 구성된다.
- Vue
    - DOM Listneners = View 의 이벤트를 청취하여 JavaScript의 데이터를 바꿔주거나 특정 로직을 실행한다
    - Data Biindings = JavaScript에서 관련 로직을 실행하고 View에 반영한다

![Untitled](/images/vue_concept/Untitled.png)

- 참고 자료
    - 설치 및 정리 : [https://joshua1988.github.io/vue-camp/vue/router.html#뷰-라우터-설치](https://joshua1988.github.io/vue-camp/vue/router.html#%E1%84%87%E1%85%B2-%E1%84%85%E1%85%A1%E1%84%8B%E1%85%AE%E1%84%90%E1%85%A5-%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5)

### 실습1

- 폴더 생성
- 파일 생성 : web-dev.html
- 기본 코드 생성 :   **! + TAB**
- 패널 토글 : **Ctrl + \**
- 쉽게 작성 예시 : **div#app 입력한 후에 Enter**

- console.log 가 div 태그의 정보를 받아와서 출력한다

```jsx
<div id="app"></div>

  <script>
      
      var div = document.querySelector('#app');
      console.log(div);
			div.innerHTML = 'hello world';

			str = 'hello world!!!';  // 여기까지만 작성하면 !!!는 반영되지 않는다
      div.innerHTML = str;
  </script>
```

- 서버 실행
- F12
- Console 칸에서 결과 확인

![Untitled](/images/vue_concept/Untitled%201.png)

### 실습2

- 파일 생성 : vue-way.html
- ***Object.defineProperty*** 라는 API 사용
    - **객체의 특정 속성을 재정의**
    - [https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)
- 사용법

```jsx
Object.defineProperty(대상 객체, 객체의 속성, {

            
        })
```

- 사용 예시

```jsx
<div id="app"></div>

    <script>
      var div = document.querySelector('#app');
      var viewModel = {};

      Object.defineProperty(viewModel, 'str', {
            // 속성에 접글했을 때의 동작을 정의
            get: function(){
                console.log('접근');

            },
            // 속성에 값을 할당했을 때의 동작을 정의
            set: function(newValue){
                console.log('할당', newValue); 

            }

          })
    </script>
```

- 결과

![Untitled](/images/vue_concept/Untitled%202.png)

- set:function 수정

```jsx
// 속성에 값을 할당했을 때의 동작을 정의
  set: function(newValue){
      console.log('할당', newValue); 
      **div.innerHTML = newValue;**
  }
```

- 결과
- **실행 결과 곧바로 화면에 반영!**
- **data binding**
    - = Re Activity 특성

![Untitled](/images/vue_concept/Untitled%203.png)

- 위에서 작성한 코드를 함수에 담는다
- 그 함수를 **즉시 실행 함수** 문법에 담는다 : `(function() {    …   } )();`
    - 즉시 실행 함수 링크
    - [https://developer.mozilla.org/ko/docs/Glossary/IIFE](https://developer.mozilla.org/ko/docs/Glossary/IIFE)
- `div.innerHTML = newValue;` 부분을 `render(newValue)`로 대체한다

```jsx
(function() {
            function init() {

                Object.defineProperty(viewModel, 'str', {
                    // 속성에 접글했을 때의 동작을 정의
                    get: function () {
                        console.log('접근');

                    },
                    // 속성에 값을 할당했을 때의 동작을 정의
                    set: function (newValue) {
                        console.log('할당', newValue);
                        // div.innerHTML = newValue;
                        **render(newValue);**
                    }
                });
            }

            function **render**(value) {
                div.innerHTML = value;
            }

            init();

        })();
```

- 결과

![Untitled](/images/vue_concept/Untitled%204.png)

### Vue 개발자 도구 사용법

- getting-started → index.html
- vue.js 스크립트를 들고 와서 실행하는 간단한 코드

```jsx
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Getting Started</title>
  </head>
  <body>
    <div id="app">
      {{ message }}
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
      new Vue({
        el: '#app',
        data: {
          message: 'Hello Vue.js'
        }
      })
    </script>
  </body>
</html>
```

- 라이브 서버 실행
- Vue 개발자 도구 확인
    - Vue → Components
    
    ![Untitled](/images/vue_concept/Untitled%205.png)
    
- data 변경 가능
    - 화면에 반영된다

![Untitled](/images/vue_concept/Untitled%206.png)

---

### Slot

- 특정 태그에서 문자를 선택적으로 출력할 때 사용 가능??
- 문서를 정독하는 게 빠를 듯하다
- 공식 문서 : [https://v2.ko.vuejs.org/v2/guide/components-slots.html](https://v2.ko.vuejs.org/v2/guide/components-slots.html)
- 참고용 : [https://kyounghwan01.github.io/blog/Vue/vue/slot/#기본](https://kyounghwan01.github.io/blog/Vue/vue/slot/#%E1%84%80%E1%85%B5%E1%84%87%E1%85%A9%E1%86%AB)

### 랜더링(Rendering)

- 읽어들인 코드를 웹 표준에 맞게, 화면에 적절히 그려내는 중요 구성요소
- 즉, HTML, CSS, JS 등을 통해 만든 페이지가 브라우저에서 보여지게 되는 것
- [https://velog.io/@plum3526/랜더링Rendering](https://velog.io/@plum3526/%EB%9E%9C%EB%8D%94%EB%A7%81Rendering)