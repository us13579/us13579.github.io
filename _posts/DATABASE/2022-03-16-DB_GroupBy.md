---
layout: single
title:  "DATABASE Group by 절"
categories: 
    - DATABASE
tags: 
    - [2022-03, DATABASE, STUDY]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">DB ( DataBase )</a>
<img width="100%" src="./../../images/db.png">

## <a style="color:#00adb5">Group by 절</a>
- select 문에서 group by 절을 사용하는 경우 database 는 <a style="color:red"><strong>쿼리 된 테이블의 행을 그룹으로 묶는다.</strong></a>
- database 는 선택 목록의 집계 함수를 각 행 그룹에 적용하고 각 그룹에 대해 단일 결과 행을 반환한다.
- group by 절을 생략하면 database 는 선택 목록의 집계 함수를 쿼리 된 테이블의 모든 행에 적용한다.
- select 절의 모든 요소는 group by 절의 표현식, 집계 함수를 포함하는 표현식 또는 상수만 가능하다.

<br>
<figure style="text-align:center;">
<figcaption style="color:red; font-weight:bold; font-size:25px">실행순서</figcaption><br>
<img width="100%" src="./../../images/select.png">
</figure>

### <a style="color:#00adb5">예시</a>

- 부서번호, 부서별 급여의 총합, 평균 급여

```sql

select department_id, sum(salary), avg(salary)
from employees;
group by department_id;

-> 부서별로 구하기 때문에 부서로 그룹핑을 해준다
```

- 각 부서별 최고 급여를 받는 사원의 부서번호, 사번, 이름, 급여 
    - <a style="color:red"><strong>join</strong></a> 사용

```sql

select a.department_id, e.employee_id, e.first_name, a.smax
from employees e join (
    select department_id, max(salary) as smax
    from employees
    group by department_id
    ) a
on e.department_id = a.department_id
and e.salary = a.smax;
```



- 각 부서별 최고 급여를 받는 사원의 부서번호, 사번, 이름, 급여
    - <a style="color:red"><strong>다중 컬럼 subquery</strong></a> 사용

```sql

select department_id, employee_id, first_name, salary
from employees
where (department_id, salary) in ( select department_id, max(salary)
                                   from employees
                                   group by department_id )
order by department_id;
```



### <a style="color:#00adb5">Having 절</a>
- group by 한 결과에 조건을 추가할 경우 having 절을 사용한다.
- Query의 실행 순서를 보면 where 절이 group by 절보다 먼저 실행되기 때문에 Aggregate ( sum, avg .. ) 조건은 having 절에 작성한다.

```sql
- 부서별 평균 급여가 7000이상인 부서 번호, 평균 급여
select department_id, avg(salary)
from employees
group by department_id
having avg(salary) >= 7000;
```

- Having 절에서 subquery

```sql
- 부서별 평균 급여가 20번 부서의 평균 급여보다 큰 부서의 부서번호, 평균 급여

select department_id, avg(salary)
from employees
group by department_id
having avg(salary) > (
    select avg(salary)
    from employees
    where department_id = 20
    );

-> subquery에서 평균 하나만 구하면 되기 때문에 group by를 해줄 필요가 없다
```

### <a style="color:#00adb5">SET ( 집합 연산자 ) </a>
- 모든 집합 연산자는 동일한 우선 순위를 갖는다.
- select 절에 있는 <a style="color:red"><strong>column 개수와 type이 일치</strong></a>해야 한다.

```sql
select col_name1
from table_name1

set 연산자

select col_name2
from table_name2

```

#### <a style="color:#00adb5">UNION </a>
두 쿼리에서 선택된 모든 행 반환 ( 중복은 한번만 )<br>
<a style="color:red"><strong>합집합</strong></a>

#### <a style="color:#00adb5">UNION ALL</a>
두 쿼리에서 선택된 모든 행 반환 ( 모든 중복 포함 )<br>
<a style="color:red"><strong>합집합</strong></a>

#### <a style="color:#00adb5">INTERSECT </a>
두 쿼리에서 선택된 모든 중복 행 반환<br>
<a style="color:red"><strong>교집합</strong></a>

#### <a style="color:#00adb5">MINUS </a>
하나의 쿼리에서 다른 하나의 쿼리를 제거. 첫번째 쿼리에만 있는 내용을 출력<br>
<a style="color:red"><strong>차집합</strong></a>

## <a style="color:#00adb5">DATABASE</a> Group by 마무리
SQL 문에서의 Group by 절에 대해 공부해 보았다.<br>
그룹을 만들고 HAVING 절로 조건을 추가하는 구조이다.<br>
가져오고 싶은 데이터가 무엇인지에 따라 그룹화 해야하는 것이 다르기 때문에 잘 파악해서 사용해야 한다.<br>
그리고 연산자도 쓰일 때가 종종 있으니 잘 알고있으면 좋을 것 같다.