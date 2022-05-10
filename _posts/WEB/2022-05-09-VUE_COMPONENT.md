---
layout: single
title: "Vue.js_Component"
categories:
  - WEB
tags:
  - [2022-05, WEB, VUE, FRONTEND, FRAMEWORK, JAVASCRIPT]
sidebar:
  nav: "docs"
---

# 📚 <a style="color:#00adb5">Vue.js</a>

<center>
<img width="90%" src="./../../images/vue.png">
</center>
<br>

# 📚 <a style="color:#00adb5">Vue.js Component</a>

## <a style="color:#00adb5">Vue Component</a>

- Vue의 가장 강력한 기능 중 하나
- <a style="color:red"><strong>HTML Element를 확장하여 재사용 가능한 코드를 캡슐화</strong></a>
- Vue의 컴파일러에 의해 동작이 추가된 사용자 지정 엘리먼트
- Vue Component는 Vue Instance이기도 하기 때문에 모든 옵션 객체를 사용
- Life Cycle Hook 사용 가능
- 전역 컴포넌트와 지역 컴포넌트

<br>
<center>
<img width="70%" src="./../../images/component.jpg">
</center>
<br>

## <a style="color:#00adb5">전역 Component</a>

- 전역 컴포넌트를 등록하려면 <a style="color:red"><strong>Vue.component( tagName, options ) 을 사용한다.</strong></a><br>
- 권장하는 컴포넌트 이름은 <big>케밥 표기법</big>이다 ( 전부 소문자, - )
- <big>component</big>

### <a style="color:#00adb5">전역 Component 예시</a>

```html
<div id="app">
  <my-global></my-global>
  <my-global></my-global>
</div>

<script>
  Vue.component("MyGlobal", {
    template: `<h2>전역 컴포넌트입니다.</h2>`,
  });
  new Vue({
    el: "#app",
  });
</script>
```

- 출력화면

<br>
<center>
<img width="50%" src="./../../images/component1.png">
</center>
<br>

## <a style="color:#00adb5">지역 Component</a>

- 컴포넌트를 <a style="color:red"><strong>components</strong></a> 인스턴스 옵션으로 등록함으로써 다른 인스턴스/컴포넌트의 범위에서만 사용할 수 있는 컴포넌트
- <big>components</big>

### <a style="color:#00adb5">지역 Component 예시</a>

```html
<div id="app">
  <my-local></my-local>
  <my-local></my-local>
</div>
<div id="app2">
  <my-local></my-local>
  <my-local></my-local>
</div>

<script>
  new Vue({
    el: "#app",
    components: {
      "my-local": {
        template: `<h2>지역 컴포넌트입니다.</h2>`,
      },
    },
  });

  new Vue({
    el: "#app2",
  });
</script>
```

<br>
'app' 에서 component를 등록했기 때문에 'app2'에서는 component가 출력되지 않는 것을 볼 수 있다.<br>

- 출력화면

<br>
<center>
<img width="50%" src="./../../images/component2.png">
</center>
<br>

## <a style="color:#00adb5">Data는 반드시 함수여야 한다</a>

- <big>Data</big>는 컴포넌트 인스턴스의 함수여야한다.
- 밑에 예제는 버튼을 클릭하면 숫자가 하나씩 증가하는 것이다.

```html
<h2>Component Data 실습</h2>
<div id="counter">
  <number-counter></number-counter>
  <number-counter></number-counter>
</div>
<template id="btn">
  <div>
    <span>{{ count }}</span>
    <button @click="count++">클릭</button>
  </div>
</template>

<script>
  Vue.component("NumberCounter", {
    template: "#btn",
    data() {
      return {
        count: 0,
      };
    },
  });
  new Vue({
    el: "#counter",
  });
</script>
```

<br>
<center>
<img width="50%" src="./../../images/component3.png">
</center>
<br>
