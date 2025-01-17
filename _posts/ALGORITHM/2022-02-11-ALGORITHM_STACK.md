---
layout: single
title:  "ALGORITHM_STACK ( 스택 )"
categories: 
    - ALGORITHM
tags: 
    - [2022-02, ALGORITHM, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">ALGORITHM</a>

<center>
<img width="90%" src="./../../images/algorithm.png">
</center>
<br>

# 📚 <a style="color:#00adb5">STACK</a>

## <a style="color:#00adb5">스택</a>이란 무엇인가 ?
<p align="center"><img src="./../../images/stack.gif"></p><br>
<a style="color:red"><b>물건을 쌓아 올리듯 자료를 쌓아 올린 형태의 자료구조</b></a>이다.<br>
<a style="color:red"><b>후입 선출 구조 ( Last In First Out )</b></a><br>
마지막에 삽입한 자료를 가장 먼저 꺼낸다<br><br>

스택에 자료를 삽입하거나 스택에서 자료를 꺼낼 수 있다.<br>
스택에 저장된 자료는 선형 구조를 갖는다<br>
스택은 연결리스트로 구현할 수 있다.<br>
스택은 배열과 달리 i번째 항목에 접근할 수 없다<br>
스택은 배열처럼 원소를 하나씩 옆으로 밀어 줄 필요가 없다<br>
스택은 데이터를 추가, 삭제하는 시간이 빠르다

-  선형 구조 : 자료 간의 관계가 1:1 관계를 갖는다
-  비선형 구조 : 자료 간의 관계가 1:N 관계를 갖는다 (트리)

## 주요 메서드

-  push(item) : item을 STACK에 저장한다 ( 삽입 )
-  pop() : STACK에서 자료를 꺼낸다 ( 삭제 ) <br>
삽입한 자료의 역순으로 꺼낸다
-  peek() : STACK의 TOP에 있는 원소를 반환한다 ( 꺼내는거 아님 )
-  inEmpty() : STACK이 비어있으면 True, 안 비어있으면 False
-  size() : STACK의 사이즈를 출력해준다
-  clear() : STACK의 모든 자료들을 삭제한다
-  display() : STACK 내의 모든 요소 출력

## 스택의 사용 

<a style="color:#00adb5"><b>재귀 알고리즘</b></a><br><br>
<a style="color:#00adb5"><b>웹 브라우저 방문기록</b></a><br><br>
<a style="color:#00adb5"><b>실행 취소 ( undo )</b></a><br><br>
<a style="color:#00adb5"><b>역순 문자열 만들기</b></a><br>

<hr>

<a style="color:#00adb5"><b>수식의 괄호 검사</b></a><br>

1. 괄호의 짝을 배열에 저장
2. '(' 을 만나면 push
3. ')' 을 만나면 짝 확인하고 맞으면 pop 
<hr>

<a style="color:#00adb5"><b>계산기 계산</b></a><br><br>

중위 표기법을 후위 표기법으로 바꾼 후 후위 표기법을 계산한다<br>

- 중위 표기법 -> 후기 표기법<br>

연산자 우선순위는 숫자로 표현해 놓는다.

1. 스택이 비어있으면 push
2. 스택이 안 비어있으면 입력연산와 STACK의 TOP 연산자 비교
3. TOP이 더 큰 경우 TOP을 pop 하고 입력값을 push 해준다. 그리고 TOP 값을 다시 push 해준다.
4. 입력값이 더 큰 경우 그냥 push 한다.

<br>

- 후위 표기법 계산

1. 입력이 숫자인 경우 push
2. 입력이 연산자이면 2개를 pop 해서 계산 해주고 그 결과값을 push
3. 마지막에 남은 수가 계산 결과

<hr>

<a style="color:#00adb5"><b>Function call</b></a><br><br>
프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리한다<br>

1. 함수 호출이 발생하면 정보를 스택 프레임에 저장하여 시스템 스택에 삽입
2. 함수의 실행이 끝나면 시스템 스택의 top 원소를 pop하면서 프레임에 저장되어 있던 복귀주소를 확인하고 복귀
3. 이 과정을 반복하여 전체 프로그램 수행이 종료되면 시스템 스택은 공백 스택이 된다
<hr>



<br><br><br><br>
👏 참조<br>
<a href="https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html" target=_blank>https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html/a></a>