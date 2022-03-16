---
layout: single
title:  "DATABASE MYSQL-FUNCTION"
categories: 
    - DATABASE
tags: 
    - [2022-03, DATABASE, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">DB ( DataBase )</a>
<img width="100%" src="./../../images/db.png">

## <a style="color:#00adb5">MYSQL Function</a> 내장 함수
MYSQL에서 사용하는 여러 내장 함수들이 있다.<br>
가져오려는 데이터를 <a style="color:red"><strong>JAVA에서 조건을 주는 것보다 MYSQL FUNCTION을 사용해서 주는게 더 유용</strong></a>하다.<br>

### <a style="color:#00adb5">숫자 관련 함수</a>

- <a style="color:#00adb5"><strong>ABS(숫자)</strong></a><br>
<a style="color:red"><strong>절대값</strong></a>을 반환

```sql
-> 5 0 5

select abs(-5), abs(0), abs(5)
from dual;
```

- <a style="color:#00adb5"><strong>CEILING(숫자)</strong></a><br>
값보다 큰 정수 중 <a style="color:red"><strong>가장 작은 수</strong></a><br>
ceil, ceiling 둘 다 사용 가능

```sql
-> 13 -12

select ceil(12.2), ceiling(-12.2)
from dual;
```

- <a style="color:#00adb5"><strong>FLOOR(숫자)</strong></a><br>
값보다 큰 작은 중 <a style="color:red"><strong>가장 큰 수</strong></a>

```sql
- 12 -13

select floor(12.6), floor(-12.6)
from dual;
```

- <a style="color:#00adb5"><strong>ROUND(숫자,자릿수)</strong></a><br>
숫자의 자릿수를 기준으로 <a style="color:red"><strong>반올림</strong></a>

```sql
- 1526 1526 1526.4 1530

select round(1526.366), round(1526.366, 0), round(1526.366, 1), round(1526.366, -1)
from dual;
```

- <a style="color:#00adb5"><strong>TRUNCATE(숫자,자릿수)</strong></a><br>
숫자의 자릿수를 기준으로 <a style="color:red"><strong>버림</strong></a>

```sql
- 1526 1526.3 1526.36 1520

select truncate(1526.366, 0), truncate(1526.366, 1), truncate(1526.366, 2), truncate(1526.366, -1)
from dual;
```

- <a style="color:#00adb5"><strong>POW(X,Y) or POWER(X,Y)</strong></a><br>
<a style="color:red"><strong>X의 Y승</strong></a><br>
pow, power 둘 다 사용 가능

```sql
- 8 8

select pow(2, 3), power(2, 3)
from dual;
```

- <a style="color:#00adb5"><strong>MOD(분자, 분모)</strong></a><br>
분자를 분모로 나눈 <a style="color:red"><strong>나머지</strong></a>

```sql
- 2 2

select mod(8, 3), 8 % 3
from dual;
```

- <a style="color:#00adb5"><strong>GREATEST(숫자1, 숫자2, 숫자3 ..)</strong></a><br>
주어진 수에서 <a style="color:red"><strong>가장 큰 수</strong></a>를 반환

```sql
- 9

select greatest(4, 3, 7, 5, 9)
from dual;
```

- <a style="color:#00adb5"><strong>LEAST(숫자1, 숫자2, 숫자3 ..)</strong></a><br>
주어진 수에서 <a style="color:red"><strong>가장 작은 수</strong></a>를 반환

```sql
- 3

select least(4, 3, 7, 5, 9)
from dual;
```

### <a style="color:#00adb5">문자 관련 함수</a>

- <a style="color:#00adb5"><strong>ASCII(문자)</strong></a><br>
문자의 <a style="color:red"><strong>아스키 코드 값</strong></a> 리턴

```sql
- 48 65 97

select ascii('0'), ascii('A'), ascii('a')
from dual;
```

- <a style="color:#00adb5"><strong>CONCAT('문자열1', '문자열2', '문자열3')</strong></a><br>
<a style="color:red"><strong>문자열들을 결합</strong></a>

```sql
- 100번 사원의 이름 Steven King

select concat(employee_id, '번 사윈의 이름 ', first_name, ' ', last_name)
from employees
where employee_id = 100;
```

- <a style="color:#00adb5"><strong>INSERT('문자열', 시작위치, 길이, '새로운 문자열')</strong></a><br>
문자열의 시작위치부터 길이만큼 <a style="color:red"><strong>새로운 문자열로 대치</strong></a>

```sql
- hello js !!

select insert('helloabc!!, 6, 3, 'js ')
from dual;
```

- <a style="color:#00adb5"><strong>REPLACE('문자열', '기존문자열', '바뀔문자열')</strong></a><br>
문자열 중 기존 문자열을 <a style="color:red"><strong>바뀔 문자열로 변경</strong></a>

```sql
- hello js !!

select replace('helloabc!!', 'abc', ' js ')
from dual;
```

- <a style="color:#00adb5"><strong>INSTR('문자열', '찾는 문자열')</strong></a><br>
문자열 중 <a style="color:red"><strong>찾는 문자열의 위치 값</strong></a>을 리턴

```sql
- 7

select insert('hello js !!, 'js')
from dual;
```

- <a style="color:#00adb5"><strong>MID('문자열', 시작위치, 개수)</strong></a><br>
문자열 중 <a style="color:red"><strong>시작위치부터 개수</strong></a>만큼 리턴

```sql
- js !!

select mid('hello js !!, 7, 5)
from dual;
```

- <a style="color:#00adb5"><strong>SUBSTRING('문자열', 시작위치, 개수)</strong></a><br>
문자열 중 <a style="color:red"><strong>시작위치부터 개수</strong></a>만큼 리턴

```sql
- js !!

select substring('hello js !!, 7, 5)
from dual;
```

- <a style="color:#00adb5"><strong>LTRIM('문자열')</strong></a><br>
문자열 중 <a style="color:red"><strong>왼쪽의 공백을 제거</strong></a>

```sql
- (hello js !! ) 

select ltrim(' hello js !! ')
from dual;
```

- <a style="color:#00adb5"><strong>RTRIM('문자열')</strong></a><br>
문자열 중 <a style="color:red"><strong>오른쪽의 공백을 제거</strong></a>

```sql
- ( hello js !!) 

select rtrim(' hello js !! ')
from dual;
```

- <a style="color:#00adb5"><strong>TRIM('문자열')</strong></a><br>
<a style="color:red"><strong>양쪽 모두의 공백을 제거</strong></a>

```sql
- (hello js !!) 

select trim(' hello js !! ')
from dual;
```

- <a style="color:#00adb5"><strong>LCASE('문자열') or LOWER('문자열')</strong></a><br>
모든 문자를 <a style="color:red"><strong>소문자로 변경</strong></a>

```sql
- hello js !!

select lower('HeLLo Js !!'), lcase('HeLLo Js !!')
from dual;
```

- <a style="color:#00adb5"><strong>UCASE('문자열') or UPPER('문자열')</strong></a><br>
모든 문자를 <a style="color:red"><strong>대문자로 변경</strong></a>

```sql
- HELLO JS !!

select upper('HeLLo Js !!'), ucase('HeLLo Js !!')
from dual;
```

- <a style="color:#00adb5"><strong>LEFT('문자열', 개수)</strong></a><br>
문자열 중 <a style="color:red"><strong>왼쪽에서 개수만큼 추출</strong></a>

```sql
- hello

select left('hello js !!', 5)
from dual;
```

- <a style="color:#00adb5"><strong>RIGHT('문자열', 개수)</strong></a><br>
문자열 중 <a style="color:red"><strong>오른쪽에서 개수만큼 추출</strong></a>

```sql
- js !!

select right('hello js !!', 5)
from dual;
```

- <a style="color:#00adb5"><strong>REVERSE('문자열')</strong></a><br>
문자열을 <a style="color:red"><strong>반대로 나열</strong></a>

```sql
- !! sj olleh

select reverse('hello js !!')
from dual;
```

### <a style="color:#00adb5">날짜 관련 함수</a>
- <a style="color:#00adb5"><strong>NOW() or SYSDATE() or CURRENT_TIMESTAMP()</strong></a><br>
<a style="color:red"><strong>현재 날짜와 시간 리턴</strong></a>

```sql
- 2022-03-16 21:09:17 2022-03-16 21:09:17 2022-03-16 21:09:17

select NOW(), SYSDATE(), CURRENT_TIMESTAMP()
from dual;
```

- <a style="color:#00adb5"><strong>CURDATE() or CURRENT_DATE()</strong></a><br>
<a style="color:red"><strong>현재 날짜 리턴</strong></a>

```sql
- 2022-03-16 2022-03-16 

select CURDATE(), CURRENT_DATE()
from dual;
```

- <a style="color:#00adb5"><strong>CURTIME() or CURRENT_TIME()</strong></a><br>
<a style="color:red"><strong>현재 시간 리턴</strong></a>

```sql
- 21:09:17 21:09:17

select CURTIME() or CURRENT_TIME()
from dual;
```

- <a style="color:#00adb5"><strong>DATE_ADD(날짜, INTERVAL 기준 값)</strong></a><br>
<a style="color:red"><strong>날짜에서 기준 값 만큼 더한다</strong></a>

```sql
- 23:09:17

select DATE_ADD(now(), INTERVAL 2 hour)
from dual;
```

- <a style="color:#00adb5"><strong>DATE_SUB(날짜, INTERVAL 기준 값)</strong></a><br>
<a style="color:red"><strong>날짜에서 기준 값 만큼 뺀다</strong></a>

```sql
- 18:09:17

select DATE_SUB(now(), INTERVAL 2 hour)
from dual;
```

- <a style="color:#00adb5"><strong>YEAR(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 연도 리턴</strong></a>

```sql
- 2022

select YEAR(now())
from dual;
```

- <a style="color:#00adb5"><strong>MONTH(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 월 리턴</strong></a>

```sql
- 3

select MONTH(now())
from dual;
```

- <a style="color:#00adb5"><strong>MONTHNAME(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 월을 영어로 리턴</strong></a>

```sql
- March

select MONTHNAME(now())
from dual;
```

- <a style="color:#00adb5"><strong>DAYNAME(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 요일을 영어로 리턴</strong></a>

```sql
- Wednesday

select DAYNAME(now())
from dual;
```

- <a style="color:#00adb5"><strong>DAYOFMONTH(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 월별 일자 리턴</strong></a>

```sql
- 16

select DAYOFMONTH(now())
from dual;
```

- <a style="color:#00adb5"><strong>DAYOFWEEK(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 주별 일자 리턴</strong></a>[일요일(1),월요일(2)..토요일(7)]

```sql
- 4

select DAYOFWEEK(now())
from dual;
```

- <a style="color:#00adb5"><strong>WEEKDAY(날짜)</strong></a><br>
<a style="color:red"><strong>날짜의 주별 일자 리턴</strong></a>[월요일(0),화요일(1)..일요일(6)]

```sql
- 2

select WEEKDAY(now())
from dual;
```

- <a style="color:#00adb5"><strong>DAYOFYEAR(날짜)</strong></a><br>
<a style="color:red"><strong>일년을 기준으로 한 날짜까지의 일 수</strong></a>(365일중 x일)

```sql
- 75

select DAYOFYEAR(now())
from dual;
```

- <a style="color:#00adb5"><strong>WEEK(날짜)</strong></a><br>
<a style="color:red"><strong>일년 중 몇 번째 주</strong></a>

```sql
- 11

select WEEK(now())
from dual;
```

- <a style="color:#00adb5"><strong>FROM_DAYS(날수)</strong></a><br>
<a style="color:red"><strong>00년 00월 00일부터 날 수 만큼 경과한 날의 날짜 리턴</strong></a>

- <a style="color:#00adb5"><strong>TO_DAYS(날짜)</strong></a><br>
<a style="color:red"><strong>00년 00월 00일부터 날짜까지의 일자 수 리턴</strong></a>

- <a style="color:#00adb5"><strong>DATE_FORMAT(날짜, '형식')</strong></a><br>
<a style="color:red"><strong>날짜를 형식에 맞게 리턴</strong></a>

```sql
- 2202 March 16 PM 09 09 17

select data_format(now(),'%Y %M %e %p %l %i %S')
from dual;
```

#### <a style="color:#00adb5">날짜 형식</a>

|format|description|format|description|format|description|
|------|-----------|------|-----------|------|-----------|
|%Y|년, 2020|%y|년, 20|
|%b|월, Jan..Dec|%M|월, January..December|%m|월, 01,02..12|
|%d|일, 00, 01, 02 .. 31|%e|일, 0, 1, 2 .. 31|
|%a|요일, Sun .. Sat|%W|요일, Sunday..Saturday|%w|요일, 0:일요일 .. 6:토요일|
|%p|AM or PM|%H|
|%H|시간, 01, 02 .. 23|%h|시간, 01, 02 .. 12|%l(알파벳 L 소문자)|시간, 01, 02 .. 12|
|%k|시간, 0, 1, 2 .. 23|%I(알파벳 i 대문자)|시간, 1,2 .. 12|%T|시간, 24-hours(hh:mm:ss)
|%i|분, 00..59|%S|초, 00..59|%s|초, 00..59|
|%j|1년중 X일, 001..365|

### <a style="color:#00adb5">논리 관련 함수</a>

- <a style="color:#00adb5"><strong>IF(논리식, 값1, 값2)</strong></a><br>
논리식이 <a style="color:red"><strong>참이면 값1 리턴, 거짓이면 값2 리턴</strong></a>

- <a style="color:#00adb5"><strong>IFNULL(값1, 값2)</strong></a><br>
<a style="color:red"><strong>값1이 NULL이면 값2로 대치, NULL이 아니면 값1리턴</strong></a>

- <a style="color:#00adb5"><strong>NULLIF(값1, 값2)</strong></a><br>
<a style="color:red"><strong>값1 = 값2가 true면 NULL, 그렇지 않으면 값1리턴</strong></a>

```sql
- 크다 3 b a

select if(3 > 2, '크다', '작다'), nullif(3, 3), nullif(3, 5), ifnull(null, 'b'), ifnull('a', 'b')
from dual;
```


### <a style="color:#00adb5">그룹 함수 ( Aggregation Function )</a>
집계 ( 그룹, 집합 ) 함수는 <a style="color:red"><strong>하나 이상의 행을 그룹으로 묶어 연산하여 총합, 평균 등을 하나의 결과로 반환</strong></a>한다.<br>

- <a style="color:#00adb5"><strong>SUM(필드명)</strong></a><br>
그룹의 <a style="color:red"><strong>누적 합계</strong></a>를 반환한다.

```sql
-> 급여의 총합을 검색

select sum(salary) 급여총합
from employees;
```

- <a style="color:#00adb5"><strong>AVG(필드명)</strong></a><br>
그룹의 <a style="color:red"><strong>평균</strong></a>을 반환한다.<br>
<strong>NULL 값은 제외하고 평균을 구한다 !!</strong>

```sql
-> 급여의 평균 ( 봉급 * 커미션 비 ) 을 검색 ( 소수 2자리까지 ) 
-> 커미션 비가 NULL 인 값을 빼고 계산함

select round(avg(salary * commission_pct), 2) 평균급여
from employees;

-> 커미션 비가 NULL 값인 것은 0 으로 칭하고 평균 구하기
-> 커미션 비가 NULL 인 값을 0 으로 하고 계산함

select round(avg(salary * (IFNULL(commission_pct), 0)), 2) 평균급여
from employees;
```


- <a style="color:#00adb5"><strong>COUNT(필드명)</strong></a><br>
그룹의 <a style="color:red"><strong>총 개수</strong></a>를 반환한다.<br>
<strong>NULL 값은 제외하고 카운팅 한다 !!</strong>

```sql
-> 사원수를 검색

select count(employee_id) 사원수
from employees;

-> 부서수를 검색

select count(department_id) 부서수
from employees;

-> 중복없이 부서수 검색

select count(distinct department_id) 부서수
from employees;
```



- <a style="color:#00adb5"><strong>MAX(필드명) & MIN(필드명)</strong></a><br>
그룹의 <a style="color:red"><strong>최대값과 최소값</strong></a>을 반환한다.

```sql
-> 80번 부서에서 근무하는 최대 급여, 최소 급여 검색

select max(salary) 최대급여, min(salary) 최소급여
from employees
where department_id = 80;
```