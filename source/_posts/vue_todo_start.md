---
title: "Vue To-do List"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-04-27'
---



[강의] ****Vue.js 중급 강좌 - 웹 앱 제작으로 배워보는 Vue.js, ES6, Vuex****

### 컴포넌트 생성

- TodoHeader.vue
- TodoInput.vue
- TodoFooter.vue
- TodoList.vue

### 반응형 웹

- vue-todo 프로젝트 > public > index.html
- 구글링 : `뷰포트 메타 태그가 있는 html`

```jsx
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <title><%= htmlWebpackPlugin.options.title %></title>
  </head>
  <body>
		<div id="app"></div>
    <script src="/dist/build.js"></script>
  </body>
</html>
```

### 파비콘

- 구글링 : favicon
- [파비콘 생성 사이트](https://www.favicon-generator.org/)

- src > assets > logo.png 를 favicon 사이트에 image 칸에 넣는다
- 체크박스 : Generate only 16x16 favicon.ico

![Untitled](/images/vue_todo_start/Untitled.png)

- 생성된 파비콘을 다운로드해서
- src > assets  > 경로에 가져온다

![Untitled](/images/vue_todo_start/Untitled%201.png)

- 파비콘 사용 코드도 같은 사이트를 참고
    - 위치만 변경해준다

![Untitled](/images/vue_todo_start/Untitled%202.png)

```jsx
<link rel="shortcut icon" href="/favicon.ico" type="image/x-icon">
<link rel="icon" href="/favicon.ico" type="image/x-icon">
```

### 어썸 아이콘

- 구글링 : Awesome icon
- get started → web font with Css → use Font Awesome Free CDN 에 적힌 코드를 복사해서 사용
    - 현재는 해당 웹에 변경점이 많아서 못 찾았다. 결국 구글링.

```jsx
<!-- 어썸 아이콘 : 6.3.0 버전-->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.3.0/css/all.min.css" />
```

### 구글 폰트

- 구글링 : google font ubuntu
- 원하는 서체 선택
- 우측에서 팝업되는 링크를 사용한다

![Untitled](/images/vue_todo_start/Untitled%203.png)

```jsx
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@500&display=swap" rel="stylesheet">
```

### index.html

- 모두 적용한 코드
- 의문점 - 어떤 방식으로 적용되는가?

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue-todo</title>
    <!-- 파비콘 -->
    <link rel="shortcut icon" href="src/assets/favicon.ico" type="image/x-icon">
    <link rel="icon" href="src/assets/favicon.ico" type="image/x-icon">

    <!-- 어썸 아이콘 -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.8.2/css/all.min.css"/>
    
    <!-- 구글 폰트 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Ubuntu:wght@500&display=swap" rel="stylesheet">
</head>
<body>
    <div id="app"></div>
    <script src="/dist/build.js"></script>
    
</body>
</html>
```

### 사용해보자

- 코드 - TodoHeader.vue

```jsx
<template>
    <header>
        <h1>TOTO it!</h1>
    </header>
</template>

<style scoped>
h1 {
    color: #2F3B52;
    font-weight: 900;
    margin: 2.5rem 0 1.5rem;
}
    
</style>
```

- 화면

![Untitled](/images/vue_todo_start/Untitled%204.png)

- <style> 에 코드 추가 - App.vue

```jsx
<style>
  body{
    text-align: center;
    background-color: F6F6F6;
  }

  input{
    border-style: groove;
    width: 200px;
  }

  button{
    border-style: groove;
  }

  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
  
</style>
```

- 결과

![Untitled](/images/vue_todo_start/Untitled%205.png)

### TodoInput.vue

- 입력한 문자가 해당 컴포넌트에 담겨야 한다
- 코드

```jsx
<template>
    <div>
        <input type="text" v-model="newTodoItem">
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            newTodoItem: ""
        }
    }
}
</script>

<style></style>
```

- 화면

![Untitled](/images/vue_todo_start/Untitled%206.png)

### 저장하는 로직

- Key - Value 형태로 저장된다

```jsx
// 저장하는 로직
localStorage.setItem();
```

- 공식문서
    - 구글링 : localStorage mdn
    - [https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)

- 코드 - TodoInput.vue

```jsx
<template>
    <div>
        <input type="text" v-model="newTodoItem">
        <button v-on:click="addTodo">add</button>
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            newTodoItem: ""
        }
    }
    , methods: {
        addTodo: function(){
            // 저장하는 로직
            localStorage.setItem(this.newTodoItem, this.newTodoItem);
            // 버튼 실행 시 input 비워주기
            this.newTodoItem = '';
        }
    }

}
</script>

<style></style>
```

- 결과
- add 버튼 클릭하고 로컬 스토리지에 저장되어있는지 확인한다
- F12 → Application → Local Storage → [http://localhos:8080/](http://localhos:8080/) 클릭

![Untitled](/images/vue_todo_start/Untitled%207.png)

### 버튼 디자인 & 적용

- 버튼 디자인 추가해서 기존의 기능도 탑재하자
- Awesome Icon에서 검색 : +

![Untitled](/images/vue_todo_start/Untitled%208.png)

- 들어가서 코드를 가져온다

- 적용
- addBtn은 기존의 기능이다
- 신기하게도 **띄어쓰기만 해도 동시에 적용** 가능한 듯 하다
- span 태그에 적용
    - input에 다음 코드 적용하면 Enter로도 가능 : *`v-on*:*keyup*.*enter*="addTodo"`

```jsx
<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem">
        <!-- <button v-on:click="addTodo">add</button> -->
        <span class="addContainer" v-on:click="addTodo">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>
    </div>
</template>
```

- 화면
- 기능도 잘 작동한다

![Untitled](/images/vue_todo_start/Untitled%209.png)

### Todo List

- 자동으로 작동하는 함수 created

```jsx
<script>
export default {
    created: function() {
        console.log('created'); 
    }
}
</script>
```

- 새로고침만 해도 적용된다

- 추가 작성
- 반복문
    - `<li **v-for**="todoItem in todoItems" **v-bind:key=**"todoItem">
         {{  todoItem }}
    </li>`
- 스토리지에 배열 저장
    - `for (var i = 0; i < localStorage.length; i++){
        if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
        this.todoItems.push(localStorage.key(i));
     } }`

```jsx
<template>
    <div>
        <ul>
            <li v-for="todoItem in todoItems" v-bind:key="todoItem">
                {{  todoItem }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    data: function(){
        return {
            todoItems: []
        }
    }
    , 
    created: function() {
        if(localStorage.length > 0){
            for (var i = 0; i < localStorage.length; i++){
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    this.todoItems.push(localStorage.key(i));
                    // console.log(localStorage.key(i));
                }
            }
        }
    }
}
</script>

<style></style>
```

- 화면

![Untitled](/images/vue_todo_start/Untitled%2010.png)

### index

- 출력된 List에 각각 다른 index를 줘야 한다
- 이미 정의된 기능이 있는 듯하다
- **함수에 매개변수로 index를 설정**하면 되는 것 같다

```jsx
<span class="removeBtn" v-on:click="removeTodo(todoItem, **index**)">
    <i class="fa-solid fa-trash-can"></i>
</span>

...
...
...

, methods: {
        removeTodo: function(todoItem, index){
            console.log(todoItem, **index**); 
        }
    }
```

- 결과
- 클릭한 List의 index가 찍힌다

### index 이용한 삭제

- local Strorage 에서 삭제한다
- 화면의 List에서 삭제한다
- 어째서??
    - 서로 다른 곳에 데이터를 담기 때문이다.
    - 그렇기에 각각 삭제해줘야 하는 것이다.

```jsx
// item 삭제 API
// Local Storage에서 삭제한다
localStorage.removeItem(todoItem); 
// JS 배열 삭제 API 
// 화면의 List에서 삭제한다
this.todoItems.splice(index, 1);
```

- icon은 Awesome icon에서 trash 검색
- 아이콘을 누르면 해당 Icon이 속한 인덱스를 통해 삭제된다

![Untitled](/images/vue_todo_start/Untitled%2011.png)

### TodoInput.vue

- 저장하는 로직에서 value에 해당하는 코드를 변경한다
- **`JSON.stringify()`**
    - 객체를 string으로 변환한다

```jsx
, methods: {
        addTodo: function(){
            var obj = {completed: false, item: this.newTodoItem};
            // 저장하는 로직
            localStorage.setItem(this.newTodoItem, **JSON.stringify(obj)**);
            // 버튼 실행 시 input 비워주기
            this.clearInput();
        }
...
```

- 입력 시 다음과 같은 형태로 들어간다

![Untitled](/images/vue_todo_start/Untitled%2012.png)

### TodoList.vue

- Local Strage 특성 상 다음과 같이 해야 한다

1. 입력할 때 key 값은 String으로 변환해야 한다 → 위에서 이미 했다
2. localStrage에 넣을 대는 JSON.parse()를 이용해야 한다
    - 이를 통해 **문자에서 객체**가 된다

```jsx
, created: function() {
        if(localStorage.length > 0){
            for (var i = 0; i < localStorage.length; i++){
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    console.log(JSON.parse(localStorage.getItem(localStorage.key(i))));

                    // this.todoItems.push(localStorage.key(i));
                    // console.log(localStorage.key(i));
                }
            }
        }
    }
```

### 값에 따라 다른 클래스 부여

- 태그에 값에 따라 다른 클래스를 줄 수 있다
- `v-bind:class="{클래스: 값}"`

```jsx
<!-- 값에 따라 다른 클래스를 줄 수 있다 v-bind:class="{클래스: 값}"-->
<i class="fa-solid fa-check checkBtn" 
						v-bind:class="{checkBtnComplete: todoItem.completed}" 
						v-on:click="toggleComplete"></i>
```

### TodoList.vue

- 전체 코드
    
    ```jsx
    <template>
        <div>
            <ul>
                 <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
                    <!-- 값에 따라 다른 클래스를 줄 수 있다 v-bind:class="{클래스: 값}"-->
                    <i class="fa-solid fa-check checkBtn" v-bind:class="{checkBtnComplete: todoItem.completed}"  
                        v-on:click="toggleComplete(todoItem, index)"></i>
                    
                    <span v-bind:class="{textCompleted: todoItem.completed}">
                        {{ todoItem.item }}
                    </span>
                    
                    <span class="removeBtn" v-on:click="removeTodo(todoItem, index)">
                        <i class="fa-solid fa-trash-can"></i>
                    </span>
                </li> 
            </ul>
        </div>
    </template>
     
    <script> 
    export default {
        data: function(){
            return {
                todoItems: []
            }
        }
        , methods: {
            removeTodo: function(todoItem, index){
                console.log(todoItem, index);
                // item 삭제 API 
                // Local Storage에서 삭제한다
                localStorage.removeItem(todoItem); 
                // JS 배열 삭제 API 
                // 화면의 List에서 삭제한다
                this.todoItems.splice(index, 1);
            }
            , toggleComplete: function(todoItem, index){
                todoItem.completed = !todoItem.completed;
                console.log(index);
                // Update 기능이 없으므로 해당 Item을 remove 후 다시 set해줘야 한다
                localStorage.removeItem(todoItem.item);
                localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
            }
        }
        , created: function() {
            if(localStorage.length > 0){
                for (var i = 0; i < localStorage.length; i++){
                    if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                        // Local Storage 특성 상, JSON.parse()를 이용해야 한다
                        this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
    
                        // this.todoItems.push(localStorage.key(i));
                        // console.log(localStorage.key(i));
                    }
                }
            }
        }
    }
    </script>
    
    <style>
    ul {
        list-style-type: none;
        padding-left: 0px;
        margin-top: 0;
        text-align: left;
    }
    li {
        display: flex;
        min-height: 50px;
        height: 50px;
        line-height: 50px;
        margin: 0.5rem 0;
        padding: 0 0 0.9rem;
        background: white;
        border-radius: 5px;
    }
    .removeBtn {
        margin-left: auto;
        color: #de4343;
    }
    .checkBox {
        line-height: 45px;
        color: #62acde;
        margin-right: 5px;
    }
    .checkBtnCompleted {
        color: #b3adad;
    }
    .textCompleted {
        text-decoration: line-through;
        color: #b3adad;
    }
    </style>
    ```
    

### TodoFooter.vue

- 버튼 클릭 시, 모든 To-do List를 지우는 기능
- 전체 코드
    
    ```jsx
    <template>
        <div class="clearAllContainer">
            <span class="clearAllBtn" v-on:click="clearTodo">
                clear All
            </span>
        </div>
    </template>
    
    <script> 
    export default {
        methods: {
            clearTodo: function(){
                localStorage.clear();
            }
        }
    }
    </script>
    
    <style scoped>
    .clearAllContainer {
        width: 8.5rem;
        height: 50px;
        line-height: 50px;
        background-color: white;
        border-radius: 5px;
        margin: 0 auto;
    } 
    .clearAllBtn {
        color: #e20303;
        /* 추가 */
        display: block;
    }
    </style>
    ```
    

### 의문점

- index.html 경로 - 강의와 다르다
- vue