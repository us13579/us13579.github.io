---
layout: single
title:  "JAVASCRIPT Basic"
categories: 
    - JAVASCRIPT
tags: 
    - [2022-03, JAVASCRIPT, STUDY]
sidebar:
    nav: "docs"
---

# <a style="color:#00adb5">JAVASCRIPT</a>
<b>웹 문서를 구성하는 3가지 요소</b>
<a style="color:red"><b>웹 페이지 이벤트 담당 ( 동 작 )</b></a><br>
<p align="center"><img src="./../../images/hcj.png"></p>

## <a style="color:#00adb5">JAVASCRIPT</a>이란 무엇인가 ?
<a style="color:red"><strong>JavaScript는 프로토타입 기반의 스크립트 프로그래밍 언어로 객체지향 개념 ( 명령형, 함수형, 프로토타입 기반 ) 을 지원</strong></a>한다.<br><br>
웹을 구성하는 요소( HTML, CSS, JavaScript ) 중 웹 브라우저에서 동작하는 <strong>유일한 프로그래밍 언어</strong>이다.<br>
그리고 개발자가 별도의 컴파일 작업을 수행하지 않는 <strong>인터프리터 언어 ( 코드를 한 줄씩 읽어 내려가며 실행하는 프로그램 ) </strong>이다. <br><br>
웹 브라우저는 HTML ( HTML + CSS ) 과 JS를 같이 다운로드 하고 브라우저의 JavaScript Engine이 JS를 실행한다.<br>
각 브라우저별 JS 엔진 ( Chrome의 V8 엔진 등 .. )은 인터프리터와 컴파일러의 장점을 결합하여 비교적 처리 속도가 느린 인터프리터의 단점을 해결해준다.<br><br>
JS는 동적으로 컨텐츠를 바꾸고 움직이는 이미지나 많은 다른 일들을 수행하게 하는 스크립트 언어이다.

## <a style="color:#00adb5">JAVASCRIPT</a>의 선언
HTML에서 JS를 사용하려면 <a style="color:red"><strong>script tag</strong></a>를 사용해야 한다.
src와 type 속성을 사용해서 JS를 선언한다.
- src<br>
외부의 JS파일을 HTML문서에 포함할 때 사용 ( 생략 가능 )
- type<br>
미디어 타입을 지정할 때, JS코드는 'text/javascript'로 지정

script tag는 HTML 파일 내부의 head 나 body 안 어느 곳에서 선언 가능하다.<br>
그러나 권장은 body 안에 끝부분에 둘 것을 권장한다. 왜냐하면 브라우저가 HTML부터 해석하여 화면에 그리기 때문에 사용자가 빠르다고 느낄 수 있다. 

### JS 코드를 HTML 문서 안에 포함

#### head tag 에 포함
```html
<html>
    <head>
        <meta charset = "UTF-8">
        <title>JavaScript 선언</title>
        <script type="text/javascript">
            // 함수 선언
            function hello(message){
                alert('hello' + message);
            }

            // 함수 호출
            hello('javascript !!');
            </script>
    </head>
    <body>

    </body>
 </html>
```

#### body tag 에 포함
body tag의 마지막에 넣는 것을 권장한다.
```html
<html>
    <head>
        <meta charset = "UTF-8">
        <title>JavaScript 선언</title>
    </head>
    <body>
            <script type="text/javascript">
            // 함수 선언
            function hello(message){
                alert('hello' + message);
            }

            // 함수 호출
            hello('javascript !!');
            </script>
    </body>
 </html>
```

### 외부 JS 파일을 HTML 문서 안에 포함
```html
<html>
    <head>
        <meta charset = "UTF-8">
        <title>JavaScript 선언</title>
        <script src = "hello.js" type="test/javascript">
        </script>
    </head>
    <body>
    </body>
 </html>
```
```javascript
hello.js 외부파일
function hello(message){
    alert('hello' + message);
    }

    // 함수 호출
     hello('javascript !!');
```

## <a style="color:#00adb5">JAVASCRIPT</a> 주석
JAVA와 주석 형태가 같다.<br>

- 한 줄 주석
```javascript
// 한 줄 주석 입니다.
```
- 블록 주석
```javascript
/*
    블록 주석
    입니다.
*/
```

## <a style="color:#00adb5">JAVASCRIPT</a> 변수
JavaScript는 <a style="color:red"><strong>동적타입 언어</strong></a>이다.<br>
그래서 변수의 타입 지정없이 값이 할당되는 과정에서 자동을 변수의 타입이 결정된다. >> 같은 변수에 여러 타입의 값을 할당 가능<br><br>
JavaScript는 <a style="color:red"><strong>낙타 표기법 ( Camel case )</strong></a>를 사용한다. 기본적으론 소문자인데 2개 이상의 단어를 사용해서 변수명을 지을 경우 2번째 단어부터 첫 글자는 대문자로 표기한다. ( ex, userName, userAge, isSelected )<br><br>
기존에는 var 키워드만 존재했었는데 ECMAScript 6부터는 let과 const 키워드가 추가되었다.<br><br>

|키워드|구분|선언위치|재선언|
|-----|----|--------|-----|
|var|변수|전역 범위|가능|
|let|변수|해당 범위|불가능|
|const|상수|해당 범위|불가능|

<br>

```javascript
    var myName = "jisoo" ;
    var age = 15;

    let count = 25;
    let name = "jisoo";
    let selected = true;

    const con = 10;
```


## <a style="color:#00adb5">JAVASCRIPT</a> 자료형

|자료형|typeof 출력 값|설명|
|:-----:|:--------------:|----|
|숫자형|number|정수 or 실수형|
|문자열형|string|문자, single or double quotation 으로 표기|
|boolean형|boolean|true or false|
|undefined|undefined|변수가 선언 되었지만 초기화가 되지 않을 경우|
|null|object|값이 존재하지 않을 경우|

<br>
undefined가 var로 변수를 선언했을 때 주의해야할 부분이다.<br>
이 부분은 밑에 <strong>변수 호이스팅</strong>에서 설명 하겠다.

### 자료형 -  <a style="color:#00adb5">숫자</a> 
정수와 실수를 구분하지 않는다.<br>
모든 숫자를 8 byte 실수 형태로 처리<br>
특정 소수점을 정확하게 표현하지 못한다.<br>
기본 연산 기호는 일반 프로그래밍 언어와 같다.<br><br>

<strong>언더플로우, 오버플로우, 0</strong>으로 나누는 연산에 대해 예외를 발생시키지 않는다.<br>
JS에서는 숫자와 관련된 특별한 상수가 존재한다.

- Infinity<br>
무한대를 나타내는 상수<br>
어떠한 수를 0으로 나누거나 Infinity를 어떠한 수로 사칙연산한 결과
- NAN ( Not A Number )<br>
계산식의 결과가 숫자가 아님을 나타내는 상수

```javascript
// 언더플로우
console.log(0 / 100);           // 0
console.log(-0 / 100);          // -0

// 오버플로우
console.log(100 / 0);           // Infinity
console.log(-100 / 0);          // Infinity
console.log(Infinity / 0);      // Infinity
console.log(-Infinity / 0);     // Infinity

// NAN  
console.log(0 / 0)              // NAN
console.log(parseInt('1A'));    // 1    
console.log(parseInt('A'));     // NAN

console.log(new Number('1'));   // 1
console.log(new Number('1A'));  // NAN
```

### 자료형 -  <a style="color:#00adb5">문자열</a> 
JS에서 문자열은 16bit의 Unicode 문자를 사용<br>
문자 하나를 표현하는 char 같은 문자형은 존재하지 않는다. 'a' 도 문자열로 표현<br>
작은 따옴표, 큰 따옴표 둘 다 사용가능이지만 혼용 불가능<br>
이스케이프 시퀀스( \\ )도 사용 가능 ( 줄바꿈 )

```javascript   
console.log("hello");           // hello
console.log('hello');           // hello
console.log("my name is "js""); //m y name is "js"
console.log("hello \nbye");     //hello
                                //bye
```

### 자료형 -  <a style="color:#00adb5">boolean, null, undefined</a> 
- boolean은 결과값으로 true, false를 갖는다.
- 비어 있는 문자열, null, undefined, 숫자 0은 false로 간주
- null은 값이 없거나 비어있음을 의미
- undefined는 값이 초기화 되지 않았음( 정의되지 않음 )을 의미
- null과 undefined는 의미가 비슷하지만 <a style="color:red"><strong>값을 할당하지 않은 변수는 undefined가 할당되고 ( 시스템 레벨 ), 코드에서 명시적으로 값이 없을을 나타낼 때 ( 프로그램 레벨 )는 null을 사용</strong></a>한다.

```javascript
var name;
var id = null;

var n1 = 10;
var n2 = 20;

console.log(n1 == n2);      // false
console.log(name);          // undefined ( 빈칸 출력 )
console.log(id);            // null
```

### 자료형 -  <a style="color:#00adb5">자동 형 변환 ( 동적 타이핑, Dynamic Typing )</a> 
JS는 자료 형에 매우 느슨한 규칙이 적용된다.<br>
<a style="color:red"><strong>'typeof 변수명'</strong></a> 으로 변수의 자료형을 알 수있다.<br>

<strong>느슨한 규칙</strong>

```javascript
var msg = 40;
console.log("40" + msg);            // 4040;
console.log("40" + 40);             // 80;

console.log(parseInt(124.45)+1);    // 125
console.log(parseFloat(124.45)+1);  // 125.45

console.log("1.1" + "1.1");         // 1.11.1
console.log(("+1.1") + ("+1.1"));         // 2.2

console.log("message " + msg);      // message 40
msg = "hello";
console.log(msg);               // hello
```

<strong>typeof 자료형</strong>

```javascript
var test;
console.log(typeof test);       // undefined

test = null;
console.log(typeof test);       // object

test = {};
console.log(typeof test);       // object

test = 3;
console.log(typeof test);       // number

test = 3.14;
console.log(typeof test);       // number

test = 'TEST';
console.log(typeof test);       // string

test = true;
console.log(typeof test);       // boolean
```

## <a style="color:#00adb5">JAVASCRIPT</a> 변수 호이스팅 ( Variable Hoisting )
var 키워드를 사용한 변수는 중복해서 선언이 가능하다.<br>
호이스팅이란 <a style="color:red"><strong>var 선언문이나 function 선언문 등 모든 선언문이 해당 범위의 처음으로 옮겨진 것처럼 동작하는 특성</strong></a>이다.<br>
즉 JS는 모든 선언문이 선언되기 이전에 참고가 가능하다.<br><br>

변수의 생성<br>
선언 단계와 초기화 단계는 한 번에 이루어진다.
- 선언 단계<br>
변수 객체에 변수를 등록한다.

- 초기화 단계<br>
변수 객체에 등록된 변수를 메모리에 할당. undefined로 초기화 된다.

- 할당 단계<br>
undefined로 초기화된 변수에 실제 값을 할당한다.

<strong>예시</strong>
```javascript
console.log(num);       // undefined
var num = 100;
console.log(num);       // 100
{
    var num = 456;
}
console.log(num);       // 456
```

먼저 제일 첫 줄인 console.log(num);은 error 가 발생할 것 같지만 콘솔에는 undefined가 출력된다. 그 이유는 <strong>모든 선언문은 Hoisting 되기 때문</strong>이다.<br>
var num = 100; 이 Hoisting 되어 첫 줄 앞에 var num; 이 옮겨진 것처럼 동작한다. 이 때 num에는 undefined로 초기화가 일어나며 나중에 var num = 100; 에서 실제로 num에 100이 할당된다. <br><br>

JS는 블록 레벨의 스코프가 아닌 함수 레벨 스코프만 갖는다. 그래서 기존 프로그래밍 언어라면 맨 마지막 줄의 출력이 100이 되어야 하는데 JS에서는 { } 안에서 선언해준 456이 출력된다.<br>

-> 해결책은 <strong>const나 let을 사용</strong>하면 된다. <br>
그래서 평소 변수 선언을 할 때도 요즘은 let을 사용하는 것이 추세이다.



## <a style="color:#00adb5">JAVASCRIPT</a> 상수 ( constant )
ECMAScript6 부터 상수 표현 지원<br>
상수 표기법은 <strong>모든 문자를 대문자를 사용</strong>하고 단어 사이는 '_'로 표기<br>
<a style="color:red"><strong>상수값은 변경하지 못한다.</strong></a>

```javascript
const LIST_COUNT = 10;
const SELECTED = false;
```

## <a style="color:#00adb5">JAVASCRIPT</a> 연산자 ( operator )
기존 JAVA 연산자랑 거의 비슷하다.<br>
다른 것 ( 많이 사용 ) - 산술, 비교, 논리, 기타

- typeof
피연산자 타입을 리턴

- ==
동등한 <strong>관계</strong>인지 확인

- !=
동등하지 않은 <strong>관계</strong>인지 확인

- ===
<strong>값이 일치</strong>하는지 확인

- !==
<strong>값이 관계</strong>하지 않는지 확인

## <a style="color:#00adb5">JAVASCRIPT</a> 조건문, 반복문 ( conditional, loop )
기존 JAVA 연산자랑 거의 같다.<br>

for문 
```javascript

for(var 변수 in 배열 or 객체){
    //실행구문
    //변수에는 배열의 인덱스
    //객체의 프로퍼티 명이 담김
}

```


## <a style="color:#00adb5">JAVASCRIPT</a> 객체 ( object )

## <a style="color:#00adb5">JAVASCRIPT</a> 함수 ( function )
JavaScript에서 함수는 <a style="color:red"><b>일급 객체(first-class)</b></a>이다.<br>
함수를 변수, 객체, 배열 등에 저장할 수 있고 다른 함수에 전달하는 인자 또는 리턴 값으로도 사용 가능하다.<br>
프로그램 실행 도중에도 동적으로 생성 가능하다.<br>

### 함수 - <a style="color:#00adb5">선언, 호출</a>

- 함수 선언문

```javascript
function 함수이름( 매개변수1, 매개변수2  ... ){
    // 함수 내용
}
```

- 함수 표현식

```javascript
var 함수이름 = function( 매개변수1, 매개변수2  ... ){
    // 함수 내용
}
```

- Function 생성자 ( constructor )

```javascript
var 함수이름 = new Function("매개변수1", "매개변수2" , ... , "함수 내용");
```

- 함수 호출

```javascript
함수이름(매개변수1, 매개변수2,...);
```


### 함수 - <a style="color:#00adb5">호이스팅</a>

- 함수 선언문<br>
함수 선언의 위치와 상관없이 코든 내 어느 곳에서든지 호출 가능<br>
함수 선언문으로 정의된 함수는 <strong>함수 선언, 초기화, 할당이 한 번에 이루어진다.</strong><br>

<a style="color:red"><b> 함수 선언문으로 함수를 정의하면 사용하기 쉽지만 ( 호이스팅을 신경 안써도 되어서 ) 대규모 application을 개발하는 경우 인터프리터가 너무 많은 코드를 변수 객체에 저장하므로 
application의 응답 속도를 저하시킬 수 있다. </b></a><br>
-> 상황에 맞게 잘 선택해서 사용하자 !


- 함수 표현식<br>
함수 호이스팅이 아니라 변수 호이스팅이 발생한다.

```javascript
var result = plus(5, 7);
console.log(result);

var plus = function(num1, num2){
    return num1 + num2;
}

// plus 함수가 밑에서 선언되어 호이스팅 발생 -> 오류 발생
```

### 함수 - <a style="color:#00adb5">매개변수</a>
외부로부터 전달받을 변수를 매개변수라 한다.<br>
타입을 명시하지 않는다.<br>
함수를 호출할 때 정의된 매개변수와 전달인자의 개수가 일치하지 않더라도 호출 가능


### 함수 - <a style="color:#00adb5">콜백 함수</a>
콜백 함수란 <strong>함수를 명시적으로 호출하는 방식이 아닌 특정 이벤트가 발생했을 때 시스템에 의해 호출되는 함수</strong><br>
일반적으로 콜백 함수는 매개변수를 통해 전달되고 전달받은 함수의 내부에서 어느 특정시점에 실행된다.<br>
주로 비동기식 처리 모델에서 사용된다.<br>
처리가 종료되면 콜백 함수를 미리 매개변수에 전달하고 처리가 종료되면 콜백 함수를 호출

- Event Handler

```html

<button id="btn">click!!</button>
<script type="text/javascript">
    var btn = document.getElementById('btn');
    btn.addEventListener('click', function (){
        console.log(' 안녕하세요');
    });
    </script>
```

- setTimeout()

```javascript

setTimeout(function () {
    console.log('3초후 실행됩니다. ');
}, 3000);

```

## <a style="color:#00adb5">JAVASCRIPT</a> 기본 마무리



