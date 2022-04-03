---
layout: single
title:  "WEB_Cookie & Session"
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

# 📚 <a style="color:#00adb5">Cookie & Session</a>
http protocol 의 특징
- client 가 server 에 요청
- server 는 요청에 대한 처리를 한 후 client에 응답
- 응답 후 연결 해제 -> <a style="color:red"><strong>stateless</strong></a>
    - 지속적인 연결로 인한 자원낭비를 줄이기 위해 연결을 해제한다.
    - 그러나 <a style="color:red"><strong>client와 server가 연결 상태를 유지해야 하는 경우 문제가 발생</strong></a> ( 로그인 정보 등 )
    - 즉 client 단위로 상태 정보를 유지해야 하는 경우 Cookie 와 Session 이 사용된다.
- HTTP Protocol 의 특징 ( 약점 ) 을 보완하기 위해 사용

# 📚 <a style="color:#00adb5">Cookie</a>

## <a style="color:#00adb5">Cookie</a> 란 무엇인가?
javax.servlet.http.Cookie<br><br>

- <a style="color:red"><strong>서버에서 사용자의 컴퓨터에 저장하는 정보 파일</strong></a>
- 사용자가 별도의 요청을 하지 않아도 브라우저는 request 시 Request Header를 넣어 자동으로 서버에 전송
- key 와 value 로 구성되고 String 형태로 이루어져 있다.
- Browser 마다 저장되는 쿠키는 다르다. ( 서버에서 브라우저가 다르면 다른 사용자로 인식한다. )

## <a style="color:#00adb5">Cookie</a> 의 사용 목적
- <strong>세션 관리</strong><br>
사용자 아이디, 접속시간, 장바구니 등의 서버가 알아야 할 정보 저장
- <strong>개인화</strong><br>
사용자마다 다르게 그 사람에 적절한 페이지를 보여줄 수 있다.
- <strong>트래킹</strong><br>
사용자의 행동과 패턴을 분석하고 기록
<br>
- 사용 예
ID 저장 ( 자동 로그인 ) , 일주일간 다시 보지 않기, 최근 검색한 상품들을 광고에 추천, 쇼핑몰 장바구니 등

## <a style="color:#00adb5">Cookie</a> 의 구성 요소
- <strong>이름</strong><br>
여러 개의 쿠키가 client의 컴퓨터에 저장되므로 각 쿠기를 구별하는 데 사용되는 이름
- <strong>값</strong><br>
쿠키의 이름과 매핑되는 값
- <strong>유효기간</strong><br>
쿠키의 유효기간
- <strong>도메인</strong><br>
쿠키를 전송할 도메인
- <strong>경로(path)</strong><br>
쿠키를 전송할 요청 경로

## <a style="color:#00adb5">Cookie</a> 의 동작 순서
1. Client 가 페이지를 요청
2. WAS는 Cookie 를 생성
3. HTTP Header에 Cookie를 넣어 응답
4. Browser는 넘겨받은 Cookie를 PC에 저장하고 다시 WAS 가 요청할 때 요청과 함께 Cookie를 전송
5. Browser가 종료되어도 Cookie의 만료 기간이 남아 있다면 Client는 계속 보관
6. 동일 사이트 재방문시 Client의 PC에 해당 Cookie가 있는 경우 요청 페이지와 함께 Cookie를 전송

## <a style="color:#00adb5">Cookie</a> 의 특징
- 이름, 값, 만료일 ( 저장 기간 설정 ), 경로 정보 로 구성되어 있다.
- 클라이언트에 총 300개의 쿠키를 저장할 수 있다.
- 하나의 도메인 당 20개의 쿠키를 가질 수 있다.
- 하나의 쿠키는 4KB까지 저장가능하다.

## <a style="color:#00adb5">Cookie</a> 의 주요 기능
- <strong>생성</strong><br>
Cookie cookie = new Cookie(String name, String value);

- <strong>값 변경, 얻기</strong><br>
cookie.setValue(String value);<br>
String value = cookie.getValue();

- <strong>사용 도메인 지정/얻기</strong><br>
cookie.setDomain(String domain);<br>
String domain = cookie.getDomain();

- <strong>값 범위지정/얻기</strong><br>
cookie.setPath(String path);<br>
String path = cookie.getPath();

- <strong>cookie의 유효기간지정/얻기</strong><br>
cookie.setMaxAge(int expiry);<br>
int expiry = cookie.getMaxAge();<br>
cookie 삭제 : cookie.setMaxAge(0);

- <strong>생성된 cookie를 client에 전송</strong><br>
response.addCookie(cookie);

- <strong>client에 저장된 cookie 얻기</strong><br>
Cookie cookies[] = request.getCookies();


# 📚 <a style="color:#00adb5">Session</a>

## <a style="color:#00adb5">Session</a> 란 무엇인가?
javax.servlet.http.HttpSession (Interface)<br><br>

- <a style="color:red"><strong>방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고 그것을 세션이라 한다.</strong></a>
- WAS의 memory에 Object의 형태로 저장
- memory가 허용하는 용량까지 제한 없이 저장 가능
<br>
- 사용 예
site내에서 화면을 이동해도 로그인 이 풀리지 않고 유지, 장바구니


## <a style="color:#00adb5">Session</a> 의 동작 순서
1. Client 가 페이지를 요청
2. 서버는 접근한 클라이언트의 Request-Header 필드인 Cookie를 확인하여, 클라이언트가 해당 session-id를 보냈는지 확인
3. session-id가 존재하지 않는다면, 서버는 session-id를 생성해 클라이언트에게 돌려준다.
4. 서버에서 클라이언트로 돌려준 session-id를 쿠키를 사용해 서버에 저장, 쿠키 이름 : JESSIONID
5. 클라이언트는 재 접속 시, 이 쿠키를 이용하여 session-id 값을 서버에 전달

## <a style="color:#00adb5">Session</a> 의 특징
- 웹 서버에 웹 컨테이너의 상태를 유지하기 위한 정보를 저장
- 웹 서버에 저장되는 쿠키 ( = 세션 쿠키)
- 브라우저를 닫거나 서버에서 세션을 삭제했을 때만 삭제가 되므로, 쿠키보다 비교적 보안이 좋다.
- 저장 데이터에 제한이 없다.
- 각 클라이언트 고유 Session ID를 부여한다.
- Session ID로 클라이언트를 구분하여 각 클라이언트 요구에 맞는 서비스를 제공한다.

## <a style="color:#00adb5">Session</a> 의 주요 기능
- <strong>생성</strong><br>
HttpSession session = request.getSession();<br>
HttpSession session = request.getSession(false);

- <strong>값 저장</strong><br>
session.setAttribute(String name, Object value);

- <strong>값 얻기</strong><br>
Object obj = session.getAttribute(String name);

- <strong>값 제거</strong><br>
session.removeAttribute(String name);   특정 이름의 속성제거<br>
session.invalidate();   binding 되어있는 모든 속성 제거 ( 자주 사용 )

- <strong>생성 시간</strong><br>
long ct = session.getCreationTime();

- <strong>마지막 접근 시간</strong><br>
long lat = session.getLastAccessedTime();


## <a style="color:#00adb5">Cookie & Session</a> 정리

<table width="100%" height="1100px" style="text-align:center; font-size:30px">
<tr style='border:3px solid #00adb5'>
<td width="20%" height="70px" style='border:3px solid #00adb5'></td>
<td width="40%" style='border:3px solid #00adb5'>Session</td>
<td width="40%" style='border:3px solid #00adb5'>Cookie</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td width="20%" height="70px" style='border:3px solid #00adb5'>Type</td>
<td width="40%" style='border:3px solid #00adb5'>javax.servlet.http.HttpSession (Interface)</td>
<td width="40%" style='border:3px solid #00adb5'>javax.servlet.http.Cookie</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>저장 위치</td>
<td style='border:3px solid #00adb5'>Server의 memory에 Object로 저장</td>
<td style='border:3px solid #00adb5'>Client 컴퓨터에 file로 저장</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>저장 형식</td>
<td style='border:3px solid #00adb5'>Object 는 모두 가능 <br>( 일반적으로 Dto, List 등 저장 )</td>
<td style='border:3px solid #00adb5'>file에 저장되기 때문에 String 형태</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>사용 예</td>
<td style='border:3px solid #00adb5'>로그인 시 사용자 정보, 장바구니 등</td>
<td style='border:3px solid #00adb5'>최근 본 상품 목록, 아이디 저장, 오늘은 그만 열기</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>용량 제한</td>
<td style='border:3px solid #00adb5'>제한 없음</td>
<td style='border:3px solid #00adb5'>도메인당 20개, 1쿠키당 4KB</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>만료 시점</td>
<td style='border:3px solid #00adb5'>알수 없음 <br> ( Client 가 로그아웃 하거나 일정 시간 동안 session 에 접근하지 않을 경우, 만료시간은 web.xml에서 설정한다. )</td>
<td style='border:3px solid #00adb5'>쿠기 저장시 설정 <br>( 설정 없을 경우 browser 종료 시 만료 )</td>
</tr>
<tr style='border:3px solid #00adb5'>
<td height="70px" style='border:3px solid #00adb5'>공통</td>
<td colspan="2">전역에 저장하기 때문에 Project 내의 모든 JSP에서 사용가능,<br> MAP 형식으로 관리하기 때문에 Key 값의 중복은 허용하지 않는다.</td>
</tr>
</table>

## <a style="color:#00adb5">Cookie & Session</a> 마무리
Cookie 와 Session 에 대해 알아 보았다.<br>
Cookie 와 Session 을 비슷한 역할을 하고 동작원리도 비슷하다. 세션도 결국 쿠키를 사용하기 때문이다.<br>
그러나 Cookie 는 서버를 전혀 사용하지 않고 Session 은 서버의 자원을 사용하는 큰 차이점을 가지고 있다.<br>
Session 이 보안적으로도 유리해서 Session 을 사용하면 되지 라고 생각할 수 있지만 무분별한 Session 사용은 서버의 메모리를 많이 차지하게 되고 그렇게 되면 속도가 느려질 수 있으므로 적절하게 Session 과 Cookie 를 사용하는 것이 좋다.<br>
저장 위치와 보안 말고도 차이점이 라이프 사이클이 있다.<br>
Cookie는 쿠키 저장 시 설정하는 만료시간이나 설정이 없으면 browser 종료 시 만료 되고<br>
Session은 Client 가 로그아웃 하거나 일정 시간동안 Session에 접근하지 않을 경우 만료된다. 만료 시간은 web.xml에서 설정한다.<br>
Cookie와 Session이 비슷한 점이 많아서 차이점을 잘 알고 있으면 좋을 것 같다.