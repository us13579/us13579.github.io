---
layout: single
title:  "SPRING_SUMMARY"
categories: 
    - FRAMEWORK
tags: 
    - [2022-04, WEB, SPRING, BACKEND, FRAMEWORK]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">SPRING</a>

<center>
<img width="90%" src="./../../images/spring.png">
</center>
<br>

# 📚 <a style="color:#00adb5">SPRING_SUMMARY</a>
*Mybatis* 를 이용한 *Spring* Project를 진행할 때 해야할 것을 내가 알아볼 수 있게 정리해보고자 한다. (spring boot 아님)<br>
spring + mybatis_spring + tomcat ..

## <a style="color:#00adb5">Project 생성</a>
- STS에서 먼저 <a style="color:red"><strong>Server ( tomcat 9.0 )</strong></a>를 연결한다.
- <a style="color:red"><strong>Spring Legact Project</strong></a> 생성 ( Spring MVC Project -> package명 생성 )
- <a style="color:red"><strong>pom.xml</strong></a>  설정 ( 버전 확인 - 프로젝트에서 mybatis, spring ... 을 쓰려고하는 것들을 설정해주는 xml -> dependency, maven 으로 버전 설정 )
- <a style="color:red"><strong>Maven Update ( force 체크 )</strong></a>  -> java 1.8로 바뀐 것 확인

##  <a style="color:#00adb5">DB 관련 업무</a>
- project/res 폴더 생성 -> DB 정보 저장 ( sql, mwb .. ) , res 는 부가적인 파일이라는 뜻을 가진다.
- webapp 에 META-INF 폴더 만들기
- <a style="color:red"><strong>context.xml</strong></a> 생성 : DB연결설정 - 이름 약속<br>

```xml
username 에는 내 DB 이름, password 는 내 DB 비번
url에서 '&'를 '&amp'로 작성해야한다.
testweb은 DB 스키마 명이다.
마지막 구문은 다음으로 web.xml을 본다는 뜻
<?xml version="1.0" encoding="UTF-8"?>
<Context>
	<Resource name="jdbc/practice" auth="Container" type="javax.sql.DataSource" 
			maxTotal="100" maxIdle="30" maxWaitMillis="10000" 
			username="root" password="1234" driverClassName="com.mysql.cj.jdbc.Driver" 	
			url="jdbc:mysql://localhost:3306/testweb?serverTimezone=UTC&amp;useUniCode=yes&amp;characterEncoding=UTF-8"/> 
    <WatchedResource>WEB-INF/web.xml</WatchedResource>
</Context>
```

## <a style="color:#00adb5">web 설정</a>

### <a style="color:#00adb5">web.xml</a>
<a style="color:red"><strong>web.xml</strong></a><br>
한글 필터 설정, throwException 처리를 해준다.<br>

- *한글 필터 설정*

```xml
	<!-- POST 방식의 한글 처리. -->
	 <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
          <param-name>encoding</param-name>
          <param-value>UTF-8</param-value>
        </init-param>
     </filter>
     
     <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
     </filter-mapping>
```

- *throwException 처리*

```xml
	<!-- DispatcherServlet이 해당 mapping을 찾지 못할 경우 NoHandlerFoundException를 throw하게 설정 -->
		<init-param>
			<param-name>throwExceptionIfNoHandlerFound</param-name>
			<param-value>true</param-value>
		</init-param>
```

### <a style="color:#00adb5">web 환경이 독립적인 bean ( 비 웹 )</a>
<a style="color:red"><strong>root-context.xml</strong></a><br>
<strong>service, mapper(dao), mybatis, aop. transaction</strong> 등 관련 bean을 등록한다.<br>
설정에 필요한 것들을 namespace에서 잘 체크해주어야 한다. 그래야 설정 가능.<br><br>


- *mybatis 설정*

```xml
	<!-- mybatis-config.xml 에서 enviornments 부분 -->
    <!-- Connection pool을 사용한다. -->
    <!-- 위에 DB 설정할때 만들어준 webapp/META-INF/context.xml 을 참조한다. -->
	<bean id="ds" class="org.springframework.jndi.JndiObjectFactoryBean">
		<property name="jndiName" value="java:comp/env/jdbc/practice"></property>
	</bean>


	<!-- mybatis -->
	<!-- SqlMapConfig.java 부분 생성 -->
	<!-- factory 만들어주기 -->
	<bean id="sqlSessionFactoryBean" class="org.mybatis.spring.SqlSessionFactoryBean">
		<!-- 위에 선언한 ds 참조 -->
		<property name="dataSource" ref="ds" />
		<!-- mybatis-config.xml 에서 mappers 부분 -->
		<!-- mapper라는 폴더 밑에 모든 xml을 읽어 오겠다 	mapper가 어딨느냐~	-->
		<property name="mapperLocations" value="classpath:mapper/*.xml" />
		
		<!-- mybatis-config.xml 에서 typeAliases 부분 -->
		<!-- config가 어딨느냐~  -->
		<!-- 폴더 경로 지정해서 연결 -->
		<!-- <property name="configLocation" value="classpath:mybatis-config.xml"/> -->
		<!-- 여기서 package 선언 -> mybatis-config.xml가 없어도된다 -->
		<property name="typeAliasesPackage" value="com.practice.guestbook.model"/>
	</bean>
	
	<!-- SqlMapConfig.java 부분 생성 -->
	<!-- default 값이 없어서 반드시 생성자를 가져가야한다 -->
	<!-- factory를 가지고 SqlSession을 만들어라 -->
	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg ref="sqlSessionFactoryBean"/>
	</bean>
```
<br>

- *component-scan 설정* <br>
model ( service, mapper ( dao )) , aop<br>
service는 @Service , dao는 @Repository 를 적어줘야하고 mapper는 interface라서 annotation이 없다.

```xml
	<context:component-scan
		base-package="com.ssafy.practice.model, com.ssafy.practice.aop" />
```

- *aop 설정*

```xml
	<aop:aspectj-autoproxy></aop:aspectj-autoproxy>
```

- *transaction 설정*

```xml
	<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
		<property name="dataSource" ref="ds"/>
	</bean>
	
	<tx:annotation-driven transaction-manager="transactionManager"/>
```

### <a style="color:#00adb5">web 관련 bean ( 웹 )</a>
<a style="color:red"><strong>servlet-context.xml</strong></a>
<strong>ViewResolver , interceptors, file</strong> 등 설정<br>

- *annotataion 활성화*

```xml
    <annotation-driven />
```

- *component-scan 설정* <br>
controller<br>
Controller는 @Controller를 적어줘야한다.

```xml
	<context:component-scan base-package="com.practice.guestbook.controller" />
```

- *ViewResolver 설정*<br>
기본적으로 구현된 부분이 있다.

```xml
	<!-- viewResolver -->
    <!-- 파일명 앞 ( prefix )에 /WEB-INF/views/ 경로가 붙고 
         파일명 뒤 ( suffix )에 .jsp 가 붙는다.
    -->
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>
```

- *경로 매핑*<br>
img, css, js 는 *DispatcherServlet을 거치면서 매핑할 필요가 없다.* ( 단지 화면단에서만 보여주는 것이기 때문 - Controller가 필요가 없다. )<br>
그래서 resources에 저장해서 경로를 설정하는 것은 매핑을 안해주는다는 의미이다.<br>
실행되면 매핑안해주고 바로 전송해준다.<br>
여기서 webapp에 resources 폴더를 생성하고 안에 img, css, js 폴더를 만들어줘야한다.<br>

```xml
	<!-- <resources mapping="/resources/**" location="/resources/" /> -->
    <!-- mapping 값으로 들어오면 location으로 연결시켜달라는 의미이다. -->
	<resources mapping="/img/**" location="/resources/img/" />
	<resources mapping="/css/**" location="/resources/css/" />
	<resources mapping="/js/**" location="/resources/js/" />

```
- *interceptor*

```xml
	<beans:bean id="confirm" class="com.practice.interceptor.ConfirmInterceptor"/>

	<interceptors>
		<interceptor>
			<!-- <mapping path="/guestbook/*"/> -->
            <!-- 매핑 경로 설정 -->
			<mapping path="/guestbook/register"/>
			<mapping path="/guestbook/modify"/>
			<mapping path="/guestbook/delete"/>
			<!-- <exclude-mapping path="/user/log*"/> -->
			
			<!-- <beans:bean class="com.ssafy.interceptor.ConfirmInterceptor"/> -->
			<beans:ref bean="confirm"/>
		</interceptor>
	</interceptors>
```
- *file*

```xml
<!-- fileUpload -->
	<beans:bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<beans:property name="defaultEncoding" value="UTF-8"/>
		<beans:property name="maxUploadSize" value="52428800"/> 
		<beans:property name="maxInMemorySize" value="1048576"/> 
	</beans:bean>

	<!-- fileDownload -->
	<beans:bean id="fileDownLoadView" class="com.practice.guestbook.view.FileDownLoadView"/>
	<beans:bean id="fileViewResolver" class="org.springframework.web.servlet.view.BeanNameViewResolver">
		<beans:property name="order" value="0" />
	</beans:bean> 
```



## <a style="color:#00adb5">응용 업무 구현</a>
이제 설정들을 다 마치고 기능들을 구현하면 된다.<br>
 .jsp -> controller -> service -> mapper -> .xml <br>
구조로 데이터가 이동하며 처리된다.

###  <a style="color:#00adb5">디버깅을 위한 Log4j 정의</a>
<a style="color:red"><strong>log4j는 Apache 에서 만든 오픈소스 라이브러리</strong></a>로 프로그램을 작성하는 도중에 로그를 남기기 위해 사용되는 자바 기반 로깅 유틸리티로 <strong>디버그용 도구</strong> 로 주로 사용된다.<br>

- *pom.xml에 log4j 추가, 확인*

```xml
	<!-- Logging -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-api</artifactId>
			<version>${org.slf4j-version}</version>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>jcl-over-slf4j</artifactId>
			<version>${org.slf4j-version}</version>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-log4j12</artifactId>
			<version>${org.slf4j-version}</version>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>${log4j-version}</version>
			<exclusions>
				<exclusion>
					<groupId>javax.mail</groupId>
					<artifactId>mail</artifactId>
				</exclusion>
				<exclusion>
					<groupId>javax.jms</groupId>
					<artifactId>jms</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jdmk</groupId>
					<artifactId>jmxtools</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jmx</groupId>
					<artifactId>jmxri</artifactId>
				</exclusion>
			</exclusions>
			<scope>runtime</scope>
		</dependency>
```
- *Log4j.xml 작성*<br>
src/main/resources밑에 <strong>log4j.xml</strong>을 만든다.<br>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE log4j:configuration PUBLIC "-//APACHE//DTD LOG4J 1.2//EN" "log4j.dtd">
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">

	<!-- Appenders -->
	<appender name="console" class="org.apache.log4j.ConsoleAppender">
		<param name="Target" value="System.out" />
		<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%d %5p [%c] %m%n" />
		</layout>
	</appender>
	
	<!-- Application Loggers -->
	<logger name="com.ssafy.guestbook">
		<level value="debug" />
	</logger>
	
	<!-- 3rdparty Loggers -->
	<logger name="org.springframework.core">
		<level value="info" />
	</logger>
	
	<logger name="org.springframework.beans">
		<level value="info" />
	</logger>
	
	<logger name="org.springframework.context">
		<level value="info" />
	</logger>

	<logger name="org.springframework.web">
		<level value="info" />
	</logger>

	<!-- Root Logger -->
	<root>
		<priority value="warn" />
		<appender-ref ref="console" />
	</root>
	
</log4j:configuration>
```

- *Log4j.xml 사용*<br>
Controller 에서 선언<br>

```java
	private static final Logger logger = LoggerFactory.getLogger(MemberController.class);
```

사용<br>

```java
	logger.debug("map : {}", map.get("userId"));
```

결과<br>

```
DEBUG [com.ssafy.guestbook.controller.MemberController] map : 1234
```
console 창에 이렇게 뜬다.<br><br>

Log4j 설정 완료 !!

###  <a style="color:#00adb5">package 생성, class 생성, xml 생성</a>
내가 하고있는 project를 따와서 예시로 든 것이다.<br>

*src/main/java*
- com.practice.guestbook.controller
    - controller 
- com.practice.guestbook.model
    - dto
- com.practice.guestbook.model.mapper
    - mapper
- com.practice.guestbook.model.service
    - service
    - serviceImpl
- com.practice.guestbook.view
    - file 관련
- com.practice.interceptor
    - interceptor
- com.practice.util
    -page 처리
<br>


*src/main/resources/mapper*
sql문 처리 xml
- member.xml
- guestbook.xml
<br>

*src/main/webapp/resources*
- img
    - img
- css
    - css 작성
- js
    - js 작성
<br>

*src/main/webapp/WEB-INF/spring*
- servlet-context.xml
- root-context.xml
<br>

*src/main/webapp/WEB-INF/views*
화면 단 ( jsp )
