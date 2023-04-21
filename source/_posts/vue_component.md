---
title: "Vue 컴포넌트"
tags:
  - Vue.js
  - Vue.js 기초
categories:
  - Vue.js
author: "minkuen"
date: '2023-04-21'
---


[인프런 강의] ****Vue.js 시작하기 - Age of Vue.js****

### Vue 컴포넌트

- **화면의 영역을 구분하여 개발**하는 기능
- 코드의 재사용성이 올라가고 빠르게 화면을 제작 가능

![Untitled](/images/vue_component/Untitled.png)

- 컴포넌트 등록 코드

```jsx
Vue.component('컴포넌트 이름', '컴포넌트 내용');
```

### 전역 Component

- 파일 생성 : component.html
- 직접 태그를 생성할 수 있다
- <div> 태그 내에 생성한 태그 적용

```jsx
<div id="app">
    <app-header></app-header>
		<app-content></app-content>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
	// 전역 컴포넌트
   Vue.component('app-header', {
        template: '<h1>Header</h1>'
    });

    Vue.component('app-content', {
        template: '<div>content</div>'
    })

    new Vue({
        el: '#app'
    });

</script>
```

- 결과
- Root 아래로 하위 Component 가 생성되었다.

![Untitled](/images/vue_component/Untitled%201.png)

### 지역 Component

- 실제로 **가장 많이 사용**되는 방식
- 문법

```jsx
// 전역 컴포넌트
Vue.component('컴포넌트 이름', 컴포넌트 내용);

// **지역 컴포넌트**
new Vue({
    el: '#app',
    components: {
        '컴포넌트 이름' : 컴포넌트 내용
    }
});
```

- 실제 지역 컴포넌트 등록, 출력

```jsx
<div id="app">
        <app-footer></app-footer>
</div>

<script>
	new Vue({
	      el: '#app',
				// 지역 컴포넌트 등록 방식
	      components: {
	          // '컴포넌트 이름' : 컴포넌트 내용
	          'app-footer': {
	              template: '<footer>footer</footer>'
	          }
	      }
	  });
</script>
```

- 결과

![Untitled](/images/vue_component/Untitled%202.png)

### Component 통신

- **프롭스 속성** : 상위에서 하위로는 데이터를 내려줌
- **이벤트 발생** : 하위에서 상위로는 이벤트를 올려줌

![Untitled](/images/vue_component/Untitled%203.png)

- 데이터의 흐름을 추적할 수 있다.
    - 이벤트는 올라간다
    - 데이터는 내려간다

![Untitled](/images/vue_component/Untitled%204.png)

### 실습

- 데이터를 내려본다
- 파일 생성 : props.html
- 코드 작성

```jsx
<script>
    var appHeader = {
        template: '<h1>header</h1>'
    }

  new Vue({
    el: '#app',
    components: {
        'app-header': appHeader
    },
    data: {
        message: 'hi'
    }
  })

</script>
```

- root에서 관리하는 데이터 (메세지 : ‘hi’ ) 가 보인다
- 해당 데이터를 app-header 컴포넌트에 내려볼 예정이다

![Untitled](/images/vue_component/Untitled%205.png)

- 문법
- `v-bind: 프롭스 속성 이름=“상위 컴포넌트의 데이터 이름”`

```jsx
<div id="app">
   <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>
</div>
```

- 코드
- **데이터를 받을 변수 이름을 설정**해주는 듯하다

```jsx
<div id="app">
    <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
    <app-header v-bind:propsdata="message"></app-header>
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    var appHeader = {
        template: '<h1>header</h1>'
        , **props: ['propsdata']**
    }

  new Vue({
    el: '#app',
    components: {
        'app-header': appHeader        
    },
    data: {
        message: 'hi'
    }
  })

</script>
```

- 결과
- Root의 데이터가 AppHeader로 잘 내려갔다

![Untitled](/images/vue_component/Untitled%206.png)

### Props 데이터

---

### 데이터 바인딩

```jsx
var appHeader = {
    template: '<h1>{{ propsdata }}</h1>'
    , props: ['propsdata']
}
```

- 결과
- Root에서 수정 시, **화면, 하위 컴포넌트에 모두 반영**된다

![Untitled](/images/vue_component/Untitled%207.png)

### 여러 데이터를 서로 다른 하위 컴포넌트에 내려보내기

---

- new Vue의 데이터 안에 변수 생성
- 태그 등록 부에 설정 추가
- 태그 출력 부에 props 설정 추가
- 데이터 바인딩

```jsx
<div id="app">
            <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
            <app-header v-bind:propsdata="message"></app-header>
            <app-content v-bind:propsdata="num"></app-content>
        </div>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

        <script>
            var appHeader = {
                template: '<h1>{{ propsdata }}</h1>'
                , props: ['propsdata']
            }
            var appContent = {
                template : '<div>{{ propsdata }}</div>'
                , props: ['propsdata']
            }

          new Vue({
            el: '#app',
            components: {
                'app-header': appHeader
                , 'app-content': appContent
            },
            data: {
                message: 'hi'
                , num: 10
            }

          })

        </script>
```

- 결과

![Untitled](/images/vue_component/Untitled%208.png)

### 이벤트 올리기

---

- 데이터는 내려 보낸다.
- 이벤트는 올려 보낸다.
- 파일 생성 : event-emit.html
- 문법 : `**v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트의 메서드 이름"**`
- 코드 작성

```jsx
<div id="app">
  <app-header></app-header>
</div>      
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

var appHeader = {
    template: '<button v-on:click="passEvent">click me</button>'
    , methods: {
        passEvent: function(){
            this.$emit('pass');
        }
    }
}

new Vue({
    el: '#app'
    , components: {
        'app-header': appHeader
    }
});

</script>
```

- 결과

- Vue → event 에서 확인가능

![Untitled](/images/vue_component/Untitled%209.png)

![Untitled](/images/vue_component/Untitled%2010.png)

### 이벤트 올리기2

---

- 버튼 클릭시 log 출력 : hihi
- pass 라는 이**벤트 발생을 조건**으로 태그에 설정 추가
- logText라는 **mothods의 실행을 태그에 설정** 추가
- 문법 : `**v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트의 메서드 이름"**`

```jsx
<div id="app">
    <!-- <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트의 메서드 이름"></app-header> -->
    <app-header v-on:pass="logText"></app-header>
</div>      
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

    var appHeader = {
        template: '<button v-on:click="passEvent">click me</button>'
        , methods: {
            passEvent: function(){
                this.$emit('pass');
            }
        }
    }

    new Vue({
        el: '#app'
        , components: {
            'app-header': appHeader
        }
        , methods: {
            logText: function(){
                console.log('hihi');
            }
        }
    });

</script>
```

- 결과

![Untitled](/images/vue_component/Untitled%2011.png)

### 이벤트 : 숫자 증가

---

- 버튼 클릭마다 숫자를 1만큼 늘려 본다
- 할 일
    - 해당 기능을 가질 버튼을 만든다
    - new Vue의 data에 숫자 데이터를 만든다
    - new Vue의 methods에 숫자 증가 함수를 만든다
    - 태그 출력 부에 조건과 실행 함수를 설정해준다
- 코드

```jsx
<div id="app">
        <!-- <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위 컴포넌트의 메서드 이름"></app-header> -->
        <app-header v-on:pass="logText"></app-header>
        <app-content v-on:increase="increaseNumber"></app-content>
    </div>      
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>

        var appHeader = {
            template: '<button v-on:click="passEvent">click me</button>'
            , methods: {
                passEvent: function(){
                    this.$emit('pass');
                }
            }
        }

        var appContent = {
                template: '<button v-on:click="addNumber">add</button>'
                , methods: {
                    addNumber : function(){
                        this.$emit('increase');
                    }
                }
            }

        new Vue({
            el: '#app'
            , components: {
                'app-header': appHeader
                , 'app-content' : appContent
            }
            , methods: {
                logText: function(){
                    console.log('hihi');
                }
                , increaseNumber: function () {
                    this.num = this.num + 1;
                } 
            }
            , data: {
                num: 10
            }
        });

    </script>
```

- 결과
- 버튼 클릭할 때마다 num값이 증가한다
- 단 event 메뉴를 갔다 와야 변경된 점이 반영된다

![Untitled](/images/vue_component/Untitled%2012.png)

### 같은 레벨에서의 컴포넌트 통신 방법

---

- 같은 레벨끼리 바로 통신은 불가능
- Root를 거쳐서 통신해야 한다

![Untitled](/images/vue_component/Untitled%2013.png)

- 파일 작성 : component-same-level.html
- 1단계 : 코드 작성- Root로 숫자 10 보내기
    - this.num을 이용해 컴포넌트의 mothods에 담긴 값 10을 넘겨준다

```jsx
<div id="app">
        <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header>
			  <app-content v-on:pass="deliverNum"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        var appHeader = {
            template: '<div>header</div>'
        }

        var appContent = {
            template: '<div>content<button v-on:click="passNum">pass</button></div>'
            , methods: {
                passNum: function(){
                    this.$emit('pass', 10);
                }
            }
        }

        new Vue({
            el: '#app'
            , components: {
                'app-header': appHeader
                , 'app-content': appContent
            }
            , data: {
                num: 0
            }
            , methods: {
                deliverNum: function(value){
                    this.num = value;
                }
            }
        })

    </script>
```

- 코드 작성
- 2단계 : 코드 작성- Root에서 해당 컴포넌트로 숫자 10 보내기
    - props속성을 정의해주고 Root에서 10을 넘겨준다

```jsx
<div id="app">
        <!-- <app-header v-bind:프롭스 속성 이름="상위 컴포넌트의 데이터 이름"></app-header> -->
        <app-header v-bind:propsdata="num"></app-header>
        <app-content v-on:pass="deliverNum"></app-content>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script> 
        var appHeader = {
            template: '<div>header</div>'
            , props: ['propsdata']

        }

        var appContent = {
            template: '<div>content<button v-on:click="passNum">pass</button></div>'
            , methods: {
                passNum: function(){
                    this.$emit('pass', 10);
                }
            }
        }

        new Vue({
            el: '#app'
            , components: {
                'app-header': appHeader
                , 'app-content': appContent
            }
            , data: {
                num: 0
            }
            , methods: {
                deliverNum: function(value){
                    this.num = value;
                }
            }
        })

    </script>
```

- 결과
- appHeader 컴포넌트에  10이 전달되었다

![Untitled](/images/vue_component/Untitled%2014.png)