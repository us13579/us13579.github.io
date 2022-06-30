---
layout: single
title: "SPRING VS SPRINGBOOT"
categories:
  - WEB
tags:
  - [2022-06, WEB, SPRING, SPRINGBOOT, BACKEND, FRAMEWORK]
sidebar:
  nav: "docs"
---

# 📚 <a style="color:#00adb5">SPRING</a>

<center>
<img width="90%" src="./../../images/spring.png">
</center>
<br>

# 📚 <a style="color:#00adb5">SPRING VS SPRINGBOOT</a>

## <a style="color:#00adb5">Spring</a> 이란

- 정확한 표현으로는 <a style="color:red"><strong>'Spring Framework'</strong></a>
- 자바에서 가장 많이 사용되는 프레임워크
- <big>DI ( 의존성 주입 ), IOC ( 제어 역전 ), AOP ( 관점 지향 프로그래밍 )</big>
- 위 요소들로 <a style="color:red"><strong>느슨한 결합</strong></a> 달성
- 느슨한 결합은 단위 테스트 수행하기 용이

많이 사용되는 대표적인 모듈

- Spring JDBC
- Spring MVC
- Spring AOP
- Spring ORM
- Spring Test
- Spring Expression Language ( SpEL )

<a href="https://us13579.github.io/web/SPRING/">👉 SPRING에 대해 더 자세히 알아보자 !</a>

## <a style="color:#00adb5">SpringBoot</a> 란

SpringBoot가 나오게 된 이유<br>

"javaSpring Boot makes it easy to create stand-alone,<br> production-grade Spring based Applications that you can 'just run'"<br>
스프링 부트는 <a style="color:red"><strong>단지 실행만 하면 되는 스프링 기반의 어플리케이션</strong></a>을 쉽게 만들 수 있다.
<br>
Spring의 단점만을 보완해서 만든 것<br>

- 자동설정 ( AutoConfiguration ) 을 이용
- 간편한 설정
- <a style="color:red"><strong>SpringBoot-Starter</strong></a>를 제공하여 자동으로 호환되는 버젼을 관리
- 편리한 의존성 관리 ( spring boot starter dependency를 통해 다양한 패키지 수용 )
- 내장 서버로 인한 간단한 배포 서버 구축

SpringBoot starter dependency

- spring-boot-starter-service : SOAP 웹 서비스
- spring-boot-starter-web : RESTful 응용 프로그램
- spring-boot-starter-test : 단위 테스트, 통합 테스트
- spring-boot-starter-jdbc : 기본적인 JDBC
- spring-boot-starter-security : 스프링 시큐리티 ( 인증, 권한 )
- spring-boot-starter-data-jpa : Spring Data JPA ( Hibernate )
- spring-boot-starter-cache : 캐시

<a href="https://us13579.github.io/web/SPRINGBOOT/">👉 SPRINGBOOT에 대해 더 자세히 알아보자 !</a>

## <a style="color:#00adb5">Spring VS SpringBoot</a>

결국 Spring과 SpringBoot의 차이점은 SpringBoot의 기능이라 할 수 있다.<br>
자동화를 통해 좀 더 개발자가 개발에 집중할 수 있게 해줌<br>

- <a style="color:red"><big>dependency ( 의존성 관리 )</big></a>

  - Spring에서 길고 버전까지 직접 다 설정해줘야 하는 의존성 관리를 <big>SpringBoot starter dependency</big>를 통해 편리하게 할 수 있다. ( 프레임 워크에서 관리 )
  - <big>SpringBoot-Starter</big>를 제공하여 자동 호환 버전 관리

- <a style="color:red"><big>내장 서버 ( Embed Tomcat )</big></a>

  - Spring에서 따로 Tomcat이나 다른 서버를 설치해야했다면 SpringBoot에서는 내장 서버로 존재해서 간편하고 서버 구동 시간이 절반 가까이 단축되었다.

- 내장 서버 덕분에 간단하게 <a style="color:red"><big>jar 파일</big></a> ( 자바 옵션만으로 )로 배포할 수 있다.

- <a style="color:red"><big>xml 설정 없이</big></a> 자바 코드를 통해 설정 가능
