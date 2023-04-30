# 웹 구조 개선 (리펙토링)

[강의] ****Vue.js 중급 강좌 - 웹 앱 제작으로 배워보는 Vue.js, ES6, Vuex****

- 현재 앱 구조가 가진 문제점
- 최신 데이터 반영이 매끄럽지 않다

![Untitled](%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20(%E1%84%85%E1%85%B5%E1%84%91%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%86%BC)%20a938c36a30c8496b9f799d4a1318f74d/Untitled.png)

- 개선한 앱 구조
- 더 매끄러운 최신 데이터 반영
- 작은 버전의 VueEx 구조

![Untitled](%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20(%E1%84%85%E1%85%B5%E1%84%91%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%86%BC)%20a938c36a30c8496b9f799d4a1318f74d/Untitled%201.png)

### 리펙토링

---

- 리스트 관련
- TodoList의 created, todoItems:[] 를 App.vue로 옮긴다
- TodoList에 props: [’propsdata’] 를 넣어서 데이터를 Root에서 내려 받는다
- TodoList의 v-for 에도 propsdata로 수정한다

- 저장 관련
- TodoInput의 저장하는 로직을 App.vue로 옮긴다
- TodoInput에서는 해당 이벤트를 $emit할 함수 addOneItem을 만든다
- App.vue에서 이벤트를 받아서 저장하는 로직이 든 함수를 실행하도록 태그를 설정

- 삭제 관련
- TodoList의 삭제하는 로직을 App.vue로 옮긴다
- TodoList에서는 해당 이벤트를 $emit할 함수를 만든다
    - 예시)
    - `removeTodo: function(todoItem, index){
                this.$emit('removeItem', todoItem, index);
            }`
- App.vue에서 이벤트를 받아서 삭제하는 로직이 든 함수를 실행하도록 태그를 설정

- 나머지도 위와 비슷한 반복이다
- 토글(completed) 관련
- clear all 관련

- 리펙토링 이후의 구조
    - 각 컴포넌트에서 이벤트를 올린다
    - App.vue에서 이벤트 올린 것을 받는다
    - 이벤트와 관련된 함수를 App.vue에서 실행한다

- **전체코드 - App.vue**
    
    ```jsx
    <template lang="">
      <div id="app">
        <TodoHeader></TodoHeader>
        <!-- <TodoInput v-on:하위 컴포넌트에서 발생시킨 이벤트 이름="현재 컴포넌트의 메서드 명"></TodoInput> -->
        <TodoInput v-on:addTodoItem="addOneItem"></TodoInput>
        <!-- <TodoList v-bind:내려보낼 속성 이름="현재 위치의 컴포넌트 데이터 속성"></TodoList> -->
        <TodoList v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></TodoList>
        <TodoFooter  v-on:clearAll="clearAllItems"></TodoFooter>
      </div>
    </template>
    
    <script>
    import TodoHeader from './components/TodoHeader.vue'
    import TodoInput from './components/TodoInput.vue'
    import TodoFooter from './components/TodoFooter.vue'
    import TodoList from './components/TodoList.vue'
    
    export default { 
      data: function(){
        return {
          todoItems: []
        }
      }
      , methods: {
          addOneItem: function(todoItem){
            console.log("dd");
            var obj = {completed: false, item: todoItem};
            // 저장하는 로직
            localStorage.setItem(todoItem, JSON.stringify(obj));
            this.todoItems.push(obj);
          }
          , removeOneItem: function(todoItem, index){
              // item 삭제 API 
              // Local Storage에서 삭제한다
              localStorage.removeItem(todoItem.item);
              // JS 배열 삭제 API 
              // 화면의 List에서 삭제한다
              this.todoItems.splice(index, 1);
          }
          , toggleOneItem: function(todoItem, index){
              todoItem.completed = !todoItem.completed; 
              console.log(index);
              // Update 기능이 없으므로 해당 Item을 remove 후 다시 set해줘야 한다
              localStorage.removeItem(todoItem.item);
              localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    
          }
          , clearAllItems: function(){
              localStorage.clear();
              this.todoItems=[];
          }
      }
      , created: function () {
        if (localStorage.length > 0) {
          for (var i = 0; i < localStorage.length; i++) {
            if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
              // Local Storage 특성 상, JSON.parse()를 이용해야 한다
              this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
            }
          }
        }
      }
      , components: {
          // 컴포넌트 태그명 : 컴포넌트 내용
          'TodoHeader': TodoHeader
          , 'TodoInput': TodoInput
          , 'TodoFooter': TodoFooter
          , 'TodoList': TodoList
        }
      
    }
    </script>
    <style>
      body{
        text-align: center;
        background-color: #F6F6F6;
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
    
- <template>의 태그에서 이벤트 받아서 실행하는 코드가 추가되었고
- <script>의 methods에 각각의 실행 함수 코드가 추가되었다

## alert( ) 디자인

---

### 모달 컴포넌트 등록

• [모달 코드 안내 링크](https://v2.vuejs.org/v2/examples/modal.html)

- 링크에서 기능을 미리 사용해보고 가져온다
- <transition> 태그 내부만 복사해온다

![Untitled](%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20(%E1%84%85%E1%85%B5%E1%84%91%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%86%BC)%20a938c36a30c8496b9f799d4a1318f74d/Untitled%202.png)

- 폴더 생성 : components > common
- 파일 생성 : components > common > Modal.vue

- <transition> 태그 내부만 복사해온 것을 <template> 태그에 넣는다
- 위 사이트의 CSS를 모두 복사해 <style>에 넣는다

- TodoInput.vue에 컴포넌트 항목 추가
    - Modal.vue를 하위 컴포넌트로 설정한다
    
    ```
    , components: {
            Modal : Modal
        }
    ```
    
- TodoInput.vue에 import 추가
    - *`import* Modal *from* './common/Modal.vue'`

- 공식 사이트에서<modal> 부분을 가져온다
- 단 우리 쪽에 맞춰서 태그를 <Modal>로 해준다. 대문자로 변경한 것

```jsx
<Modal v-if="showModal" @close="showModal = false">
	<h3 slot="header">custom header</h3>
</Modal>
```

### 공식문서 사용

- *리스트 아이템 트랜지션 효과*
    - [Enter/Leave & List Transitions — Vue.js (vuejs.org)](https://v2.vuejs.org/v2/guide/transitions.html#List-Entering-Leaving-Transitions)
    - CSS 다 적용해주고
    - <Transition> 태그로 원하는 부분 감싸주면 된다
    - 천천히 To-do LIst에 추가되는 효과가 생긴다

![Untitled](%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9%20%E1%84%80%E1%85%A2%E1%84%89%E1%85%A5%E1%86%AB%20(%E1%84%85%E1%85%B5%E1%84%91%E1%85%A6%E1%86%A8%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%86%BC)%20a938c36a30c8496b9f799d4a1318f74d/Untitled%203.png)