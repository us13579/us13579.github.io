---
layout: single
title:  "WEB_SERVLET"
categories: 
    - WEB
tags: 
    - [2022-03, DATABASE, WEB]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">WEB</a>

<center>
<img width="90%" src="./../../images/webb.jpg">
</center>
<br>

# 📚 <a style="color:#00adb5">SERVLET</a>

## <a style="color:#00adb5">SERVLET</a> 이란 무엇인가?
자바 서블릿 ( JAVA Servlet ) 은 <a style="color:red"><strong>자바를 사용하여 웹 페이지를 동적으로 생성하는 서버측 프로그램 혹은 그 사양</strong></a>을 말한다.<br>
자바 서블릿은 웹 서버의 성능을 향상하기 위해 사용되는 자바 클래스의 일종이다.<br>
서블릿은 자바로 구현된 CGI 이다.<br>
CGI는 특별한 라이브러리나 도구가 아니고 별도로 제작된 웹서버와 프로그램간의 교환방식이다.<br>
자바 서블릿은 JSP와 비슷한 점이 있지만 <a style="color:red"><strong>자바 서블릿은 자바 코드안에 HTML을 포함</strong></a>하고 있고, <a style="color:red"><strong>JSP는 HTML안에 자바 코드를 포함</strong></a>하고 있다.

## <a style="color:#00adb5">SERVLET</a> 의 특징
- 클라이언트의 요청에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- html을 사용하여 요청에 응답한다.
- java thread를 이용하여 동작한다.
- MVC 패턴에서 Controller로 이용된다.
- HTTP 프로토콜 서비스를 지원하는 javax.servlet.http.HttpServlet 클래스를 상속받는다.
- UDP보다 처리 속도가 느리다.
- HTML 번경 시 Servlet을 재컴파일해야하는 단점이 있다.

## <a style="color:#00adb5">SERVLET</a> 의 동작과정

<center>
<img width="90%" src="./../../images/servlet.png">
</center>
<br>

1. 사용자 ( Client )가 URL을 입력하면 HTTP Request가 Servlet Container로 전송합니다.
2. 요청을 전송받은 Servlet Container는 HttpServletRequest, HttpServletResponse 객체를 생성한다.
3. web.xml을 기반으로 사용자가 요청한 URL이 어느 서블릿에 대한 요청인지 찾는다.
4. 해당 서블릿에서 service 메서드를 호출한 후 클라이언트의 GET, POST 여부에 따라 doGet() 또는 doPost()를 호출한다.
5. doGet() or doPost() 메서드는 동적 페이지를 생성한 후 HttpServletResponse객체에 응답을 보낸다.
6. 응답이 끝나면 HttpServletRequest, HttpServletResponse 두 객체를 소멸시킨다.

## <a style="color:#00adb5">SERVLET</a> API

<center>
<img width="90%" src="./../../images/servletAPI.png">
</center>
<br>

## <a style="color:#00adb5">SERVLET</a> Life-Cycle
Servlet class는 javaSE에서의 class와는 다르게 main method가 없다. 즉 <a style="color:red"><strong>객체의 생성부터 사용의 주체가 사용자가 아닌 Servlet Container에게 있다.</strong></a><br>
Client가 요청(request) 하게 되면 Servlet Container는 Servlet 객체를 생성 (한번만)하고, 초기화 (한번만) 하며 요청에 대한 처리 ( 요청시마다 반복 )를 하게 된다. 또한 Servlet 객체가 필요없게 되면 제거하는 일까지 Container가 담당한다.

### <a style="color:#00adb5">SERVLET</a> Life-Cycle의 주요 메서드

<center>
<img width="90%" src="./../../images/servletCycle.png">
</center>
<br>

- init()<br>
서블릿이 메모리에 로드 될 때 한 번 호출<br>
코드 수정으로 다시 로드 되면 다시 호출

- doGet()<br>
GET방식으로 data 전송 시 호출

- doPost()<br>
POST방식으로 data 전송 시 호출

- service()<br>
모든 요청은 service()를 통해서 doXXX() 메서드로 이동

- destroy()<br>
서블릿이 메모리에서 해제되면 호출<br>
코드가 수정되면 호출


## <a style="color:#00adb5">SERVLET</a> Parameter

### <a style="color:#00adb5">GET</a> 

- 특징<br>
전송되는 데이터가 URL뒤에 Query String으로 전달.<br>
입력 값이 적은 경우나 데이터가 노출이 되도 문제가 없을 경우 사용

- 장점<br>
간단한 데이터를 빠르게 전송<br>
form tag 뿐만 아니라 직접 URL에 입력하여 전송 가능

- 단점<br>
데이터 양에 제한이 있다.<br>

### <a style="color:#00adb5">POST</a> 

- 특징<br>
URL과 별도로 전송<br>
HTTP header 뒤 body에 입력 스트림 데이터로 전달

- 장점<br>
데이터의 제한이 없다.<br>
최소한의 보안 유지 효과를 볼 수 있다.

- 단점<br>
전날 데이터의 양이 같을 경우 GET방식 보다 느리다.

## <a style="color:#00adb5">URL ? </a>

<center>
<img width="90%" src="./../../images/url.png">
</center>
<br>


## <a style="color:#00adb5">SERVLET</a> 마무리
자바 서블릿에 대해 알아보았다.<br>
솔직히 현재에는 거의 안쓰인다지만 웹 개발의 역사에 있기 때문에 영향들이 있을 거라고 생각한다.<br>
그건 사실 더 배워봐야 알겠지만 ㅎㅎ<br>
실습도 해보았는데 확실히 웹 들어오니까 왔다갔다 헷갈리는게 좀 많다..<br>
그리고 자바를 왜 착실히 해놓으라는지 알 것 같다.<br>
해결하기 위한 방법이 다 자바기 때문에 자바를 잘 알고 있지 않으면 방법을 알아도 해결하지 못하는 상황이 발생할 것 같다.<br>
그리고 servlet은 java 코드안에 HTML을 작성하기 때문에 굉장히 번거로운 작업들이 존재한다.<br>
그것들을 해소해주고 좀 더 유용한 방법인 JSP 를 더 알아보도록 하자.


<br><br><br><br>
👏 참조<br>
<a href="https://mangkyu.tistory.com/14" target=_blank>https://mangkyu.tistory.com/14</a><br>