---
layout: single
title: "Vue.js_Router"
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

# 📚 <a style="color:#00adb5">Vue.js Router</a>

## <a style="color:#00adb5">Vue Router</a>

- <big>라우팅</big> : <a style="color:red"><strong>웹 페이지 간의 이동 방법</strong></a>
- Vue.js 의 공식 라우터
- 라우터는 컴포넌트와 매핑
- Vue를 이용한 SPA를 제작할 때 유용
- URL에 따라 컴포넌트를 연결하고 설정된 컴포넌트를 보여준다.

## <a style="color:#00adb5">Vue Router 설치</a>

- CDN 방식

  - `<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>`
  - `<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>`

- NPM 방식 ( 주 )
  - npm install vue-router

## <a style="color:#00adb5">Vue Router 연결</a>

- <a style="color:red"><strong>routes</strong></a> 옵션과 함께 <a style="color:red"><strong>router instance 생성</strong></a>

```javascript
const Main = {
  template: `<div>메인 페이지</div>`,
};

const Board = {
  template: `<div>자유 게시판</div>`,
};

const router = new VueRouter({
  // 라우트 컴포넌트 정의
  routes: [
    {
      path: "/",
      component: Main,
    },
    {
      path: "/board",
      component: Board,
    },
  ],
});
```

## <a style="color:#00adb5">Vue Router 이동 및 랜더링</a>

- <big>랜더링</big>이란 HTML,CSS,JS 등 개발자가 작성한 문서를 브라우저에서 그래픽 형태로 출력하는 과정을 말한다.
- 네비게이션을 위해 <a style="color:red"><strong>router-link</strong></a> 컴포넌트 사용
- 속성은 <a style="color:red"><strong>'to' prop</strong></a> 을 사용
- 기본적으로 `<router-link>` 는 `<a>` 태그로 렌더링

```html
<router-link to="/">HOME</router-link>
<router-link to="/board">게시판</router-link>
```

- 현재 라우트에 맞는 컴포넌트가 렌더링 된다.

```html
<!-- 현재 라우트에 맞는 컴포넌트가 랜더링 -->
<router-view></router-view>
```

## <a style="color:#00adb5">Vue Router 설정</a>

### <a style="color:#00adb5">라우터 설정</a>

```javascript
const router = new VueRouter({
  routes: [
    ...,
    {
      path: '/board/:no',
      component: BoardView,
    },
    ...,
  ],
});
```

- 라우터 링크

```html
<router-link to="/board/30">30번 게시글</router-link>
```

- <big>전체 라우터 정보</big>

  - `this.$router`

- <big>현재 호출된 라우터 정보</big>

  - `this.$route`
  - `this.$route.params.no`
  - `this.$route.path`

### <a style="color:#00adb5">이름을 가지는 라우트</a>

- 라우트는 연결하거나 탐색을 수행할 때 <big>이름이 있는 라우트</big>를 사용
- Router Instance를 생성하는 동안 routes 옵션에 지정

```javascript
const router = new VueRouter({
  routes: [
    ...,
    {
      path: '/board',
      name: 'board',
      component: Board,
    },
    {
      path: '/board/:no',
      name: 'boardview',
      component: BoardView,
    },
    ...,
  ],
});
```

```html
<!-- 두 개다 같은 것을 호출한다 -->
<router-link :to="{name: 'boardview', params: {no: 3}}">3번 게시글</router-link>
<a @click="$router.push({name: 'boardview', params: {no: 3}});">3번 게시글</router-link>
```

### <a style="color:#00adb5">프로그래밍 방식 라우터</a>

- `<router-link>`를 사용하여 선언적 네비게이션용 anchor 태그를 만드는 것 외에도 라우터의 instance method를 사용하여 프로그래밍으로 수행

```js
$router.push("home");
$router.push({ path: "home" });
// param을 받아올 때
$router.push({ name: "boardview", params: { no: 3 } });
// query를 받아올 때
$router.push({ path: "/board", query: { pg: 1 } });
```

## <a style="color:#00adb5">중첩된 라우트</a>

- 앱 UI는 일반적으로 <a style="color:red"><strong>여러 단계로 중첩된 컴포넌트 구조</strong></a>임
- URL의 세그먼트가 중첩 된 컴포넌트의 특정 구조와 일치하는 것을 활용
- 예를 들면 게시판 ( board ) 페이지에서 비동기 통신을 통해 컴포넌트를 교체하는 경우 children 배열에 넣음으로써 중첩 된 컴포넌트 구조를 가지게 된다.
- <big>router/index.js</big>에 주로 구현한다.

```js
// 라우트 컴포넌트
import HomeView from "@/views/HomeView.vue";
import LoginView from "@/views/LoginView.vue";
import BoardView from "@/views/BoardView.vue";
import BoardList from "@/components/board/BoardList.vue";
import BoardWrite from "@/components/board/BoardWrite.vue";
import BoardDetail from "@/components/board/BoardDetail.vue";
import BoardModify from "@/components/board/BoardModify.vue";
import BoardDelete from "@/components/board/BoardDelete.vue";

routes: [
  ...,
  {
    path: '/board',
    name: 'board',
    component: BoardView,
    redirect: '/board/list',
    children: [
      // 게시판 목록
      {
        path: 'list',
        name: 'boardlist',
        component: BoardList,
      },
      // 게시판 글쓰기
      {
        path: 'write',
        name: 'boardwrite',
        component: BoardWrite,
      },
      ...
    ],
  },
],
```

## <a style="color:#00adb5">라우트 리다이렉트</a>

- 웹 페이지 이동

```js
routes: [
  ...,
  {
    path: '/board',
    name: 'board',
    component: Board,
    // component를 실행하면 /board/list 페이지로 이동한다
    redirect: '/board/list',    or redirect: { name: 'list' }
    children: [
      ...
    ],
  },
],
```
