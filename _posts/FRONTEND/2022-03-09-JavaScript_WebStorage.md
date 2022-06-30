---
layout: single
title:  "JAVASCRIPT_Web Storage"
categories: 
    - JAVASCRIPT
tags: 
    - [2022-03, JAVASCRIPT, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">JAVASCRIPT</a>

<center>
<img width="90%" src="./../../images/JAVASCRIPT.png">
</center>
<br>

# 📚 <a style="color:#00adb5">Web Storage</a>

## <a style="color:#00adb5">Web Storage</a>
- localStorage, SessionStorage 기본 구성
    - <a style="color:red"><strong>키 ( Key ) 와 값 ( Value )을 하나의 세트로 저장
    - 도메인과 브라우저 별로 저장
    - 값은 반드시 문자열로 저장됨

- 공통 메소드와 프로퍼티
    - <strong>setItem(key, value)</strong><br>
    key-value 쌍으로 저장

    - <strong>getItem(key)</strong><br>
    key에 해당하는 값을 리턴

    - <strong>removeItem(key)</strong><br>
    key에 해당하는 값을 삭제

    - <strong>clear()</strong><br>
    모든 값을 삭제

    - <strong>key(index)</strong><br>
    index에 해당하는 key

    - <strong>length</strong><br>
    저장된 항목의 개수


### <a style="color:#00adb5">Web Storage</a> - localStorage
- WebStorage API : LocalStorage
    - 데이터를 사용자 로컬에 보존하는 방식
    - 데이터를 저장, 덮어쓰기, 삭제 등 조작 가능
    - 자바스크립트로만 조작 가능
    - 모바일에서도 사용 가능

- Cookie와 차이점
    - 유효기간이 없고 영구적으로 이용 가능
    - 쿠키보다 더 많은 데이터 사용 가능
    - 쿠키와는 다르게 네트워크 요청 시 서버로 전송되지 않음
    - 서버가 HTTP 헤더를 통해 스토리지 객체를 조작할 수 없음 -> 자바스크립트로만 조작 가능
    - 웹 스토리지는 origin( 프로토콜, 도메인, 포트 )이 다르면 접근 불가

```html

// localStorage에 data 추가
<script>
function init(){
    // 추가 방법 3가지
    localStorage.Test = "Sample";
    localStorage["Test"] = "Sample";
    localStorage.setItem("Test", "Sample");
}
</script>


// localStorage에 data 얻기
<script>
function init(){
    // 취득 방법 3가지
    var val = localStorage.Test;
    var val = localStorage["Test"];
    var val = localStorage.getItem("Test");

    // 취득 data 출력
    document.querySelector("#result").innerHTML = val;
}
</script>


// localStorage에 data 삭제
<script>
function init(){
    // localStorage data 삭제
    localStorage.removeItem("Test");


    // localStorage data 취득
    var val = localStorage.Test;    //undefined

    // 취득 data 출력
    document.querySelector("#result").innerHTML = val;
}
</script>


// localStorage에 data 전체 삭제
<script>
function init(){
    // localStorage data 전체 삭제
    localStorage.clear();

}
</script>
```


### <a style="color:#00adb5">Web Storage</a> - sessionStorage
- <a style="color:red"><strong>SessionStorage는 현재 떠 있는 탭에서만 유지 ( 같은 페이지라도 탭이 다르면 다른 곳에 저장 )</strong></a>
- 페이지 새로고침시에는 데이터는 유지, 탭을 닫고 새로 열었을 경우 제거

- SessionStorage 사용법
    - <strong>세션 저장</strong><br>
    sessionStorage.setItem("key", value);

    - <strong>특정 세선 값 불러오기</strong><br>
    sessionStorage.getItem("key");

    - <strong>특정 세선 삭제</strong><br>
    sessionStorage.removeItem("key");

    - <strong>세션 전체 삭제</strong><br>
    sessionStorage.clear();

### <a style="color:#00adb5">Web Storage</a> localStorage VS sessionStorage
- 차이점
    - localStorage : 세션이 끊겨도 사용 가능
    - localStorage : 세션이 끊겨도 사용 가능

- sessionStorage의 경우 동일한 세션에서만 사용 가능하지만 localStorage는 세션이 끊기거나 동일한 세션이 아니더라도 사용 가능


## <a style="color:#00adb5">Web Storage</a> 마무리
localStorage와 sessionStorage에 대해 알아 보았다.<br>
데이터를 로컬에 저장해 자유롭게 사용하고 자바스크립트를 디버깅할 때도 유용하게 쓰일 것 같다 라는 생각이 들었다.