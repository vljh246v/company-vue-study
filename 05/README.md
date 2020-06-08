# 뷰 템플릿이란?

마크업 + 인스턴스 내부 사용자 정의 항목 (데이터, 로직 등) => HTML 로 변환

- 첫번째 방법
  - 지금까지 사용했던 temlate 속성
  - 내부적으로 render 함수로 변환 -> 사용자가 구현 가능함

* 두번째 방법

  - 싱글 파일 컴포넌트 체계

* 템플릿에서 사용하는 뷰 속성과 문법
  1. 데이터 바인딩
  2. 자바스크립트 표현식
  3. 디렉티브
  4. 이벤트 처리
  5. 고급 템플릿 기법

## 1. 데이터 바인딩

html 화면 요소를 뷰 인스턴스의 데이터와 연결, 주로 {{ }} 문법과 v-bind 속성이 있음

### {{ }} - 콧수염 괄호

- 흔한 템플릿 문법
- 기본적인 텍스트 삽입 방법
- 예제

```html
<!-- <div id="app" v-once> 데이터가 변경 되어도 값을 바꾸지 않으려면 v-once 속성 사용  -->
<div id="app">
  {{ message }}
</div>

<script>
  new Vue({
    el: "#app",
    data: {
      message: "Hello Vue.js!",
    },
  });
</script>
```

### v-bind

- 아이디, 클래스, 스타일 등 HTML 속성값에 뷰 데이터 값을 연결할 때 사용하는 데이터 연결 방식
- v-bind:{속성명 | props 속성명}:{데이터 속성명}

```html
<html>
  <head>
    <title>Vue Template - Data Binding</title>
  </head>
  <body>
    <div id="app">
      <p v-bind:id="idA">아이디 바인딩</p>
      <p v-bind:class="classA">클래스 바인딩</p>
      <p v-bind:style="styleA">스타일 바인딩</p>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        data: {
          idA: 10,
          classA: "container",
          styleA: "color: blue",
        },
      });
    </script>
  </body>
</html>
```

- 추가로 v-bind:id -> :id 로 축약 가능

## 2. 자바스크립트 표현식

- {{}} 표현식 내부에 자바스크립트 표현식을 넣을 수 있음

```html
<html>
  <head>
    <title>Vue Template - Javascript Expression</title>
  </head>
  <body>
    <div id="app">
      <p>{{ message }}</p>
      <p>{{ message + "!!!" }}</p>
      <p>{{ message.split('').reverse().join('') }}</p>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        data: {
          message: "Hello Vue.js!",
        },
      });
    </script>
  </body>
</html>
```

### 자바스크립트 표현식에서 주의할 점

- 선언문고 분기문은 사용할 수 없음
- 복잡한 연산은 인스턴스 내부 로직에서 처리, 간단한 연산 결과만 표시

## 3. 디렉티브

- v- 접두사를 가지는 모든 속성들 (앞에서 나온 v-bind 도 디렉티브의 한 종류)

```html
<a v-if="flag">두잇 Vue.js</a>
```

- 위 a 태그는 데이터의 flag 값에따라 보이기도 하고 안 보이기도 함
- 데이터 값 변경에 따라 요소들을 리액티브 하게 반응하게 하기 위함
- 주요 디렉티브
  - v-if : 참 거짓 여부에 따라 해당 html 태그 표시 결정
  - v-for : 뷰 데이터 개수만큼 해당 html 태그를 반복 출력
  - v-show : v-if와 유사하지만 css 효과로 단순히 안보이게만 함
  - v-bind : html 태그 속성과 데이터 속성을 연결함
  - v-on : 태그의 특정 이벤트를 감지하여 특정 메소드를 실행할 수 있음
  - v-model : 폼 에서 주로 사용되는 속성, 폼 입력값과 뷰 인스턴스 값 데이터를 즉시 동기화

```html
<html>
  <head>
    <title>Vue Template - Directives</title>
  </head>
  <body>
    <div id="app">
      <a v-if="flag">두잇 Vue.js</a>
      <ul>
        <li v-for="system in systems">{{ system }}</li>
      </ul>
      <p v-show="flag">두잇 Vue.js</p>
      <h5 v-bind:id="uid">뷰 입문서</h5>
      <button v-on:click="popupAlert">경고 창 버튼</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        data: {
          flag: true,
          systems: ["android", "ios", "window"],
          uid: 10,
        },
        methods: {
          popupAlert: function () {
            return alert("경고 창 표시");
          },
        },
      });
    </script>
  </body>
</html>
```

--

## 4. 이벤트 처리

```html
<html>
  <head>
    <title>Vue Template - Event Handling</title>
  </head>
  <body>
    <div id="app">
      <button v-on:click="clickBtn(10)">클릭</button>
      <button v-on:click="clickBtnEvent">클릭</button>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        methods: {
          clickBtn: function (num) {
            alert("clicked");
            alert("value : " + num);
          },
          clickBtnEvent: function (event) {
            console.log(event);
          },
        },
      });
    </script>
  </body>
</html>
```

- 위 코드는 button 태그에 v-on:click '디렉티브'추가
- 버튼을 클릭하면 clickBtn 메서드가 실행 되도록 지정
- 값 넘기기도 가능
- 이벤트 인자 사용 가능 -> 요소의 돔 이벤트 접근 가능

## 5. 고급 템플릿 기법

### computed 속성

- data 속성 값의 따라 다시 자동으로 연산됨
- 캐싱
- methods vs computed
  - 수동 / 자동 으로 갱신 차이
  - methods
    - 호출할 때만 수행
  - computed
    - data 값이 변경되면 자동으로 수행

### watch 속성

- 데이터 변화를 감지해 자동으로 특정 로직을 수행
- computed 속성과 유사
- computed는 간단한 연산, watch 는 비동기 처리에 적합

```html
<html>
  <head>
    <title>Vue Template - Watch</title>
  </head>
  <body>
    <div id="app">
      <input v-model="message" />
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue@2.5.2/dist/vue.js"></script>
    <script>
      new Vue({
        el: "#app",
        data: {
          message: "Hello Vue.js!",
        },
        watch: {
          message: function (data) {
            console.log("message의 값이 바뀝니다 : ", data);
          },
        },
      });
    </script>
  </body>
</html>
```

---

# 뷰 프로젝트 구성 방법

## 1. html 파일에서 뷰 코드 작성 시의 한계점

- template 부분에 마크업을 읽기가 어려움
- 한 파일에 여러 인스턴스 및 템플릿들이 있으면 작성이 어려움
- 이러한 부분을 해결한게 바로 싱글 파일 컴포넌트 체계

## 2. 싱글 파일 컴포넌트 체계

- vue 파일로 프로젝트 구조를 구성하는 방식
- vue 파일 1개 == 1개의 컴포넌트

```html
<template>
  <!-- html 태그 내용 -->
</template>
<script>
  export default {
    // 자바 스크립트 내용
  };
</script>
<style>
  /* css 내용 */
</style>
```

> 실습

# 실전 애플리케이션 만들기

## 1. 애플리케이션 컴포넌트 구조도

- 재사용 성을 위해 화면 1개를 작은 역할 단위로 쪼개는 것이 유리함
