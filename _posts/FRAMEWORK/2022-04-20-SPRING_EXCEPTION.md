---
layout: single
title:  "SPRING_EXCEPTION"
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

# 📚 <a style="color:#00adb5">EXCEPTION</a>

## <a style="color:#00adb5">Spring Exception 처리</a>
기존 Web MVC 에서는 Exception 처리는 try ~ catch문을 사용하고 <br>
에러처리는 web.xml에 error-code 구문을 이용해서 error가 났을 때 jsp로 보내서 처리를 해주었다.<br><br>

Spring에서의 Exception 처리는 크게 3가지로 나눌 수 있다.<br>
Spring에서는 DispatcherServlet에서 거의 99% 예외가 발생하기 때문에 *DispatcherServlet* 에서 HandlerExceptionResolver가 처리하는 방법들이라 할 수 있다.<br><br>

그전에 Exception 처리를 위한 설정을 보여주겠다.<br>
*Web.xml* 에 작성

```xml
<servlet>
	<init-param>
			<param-name>throwExceptionIfNoHandlerFound</param-name>
			<param-value>true</param-value>
	</init-param>
</servlet>
```
<br>
위 구문은 <strong>error ( NoHandlerFound - 404 error )를 exception으로 바꿔줄게</strong> 라는 의미로 생각하면 된다.<br>




- Controller 단에서의 처리<br>
Controller Level = @ExceptionHandler
- 전역 처리<br>
Global Level = @ControllerAdvice
- method 단위 처리<br>
Method Level = try ~ catch

<br><br>

### <a style="color:#00adb5">Controller 단에서의 처리</a>
<a style="color:red"><strong>@ExceptionHandler</strong></a> annotation을 통해 처리<br>

```java
@Controller
public class TestController{

    private static final Logger logger = LoggerFactory.getLogger(GuestBookController.class);

    @ExceptionHandler(Exception.class)
	public String handleException(Exception ex, Model model) {
		logger.error("Exception 발생 : {}", ex.getMessage());
		model.addAttribute("msg", "처리중 에러 발생!!!");
		return "error/error";
	}
}
```
<br>
<a style="color:red"><strong>*TestController* 내에서 발생하는 Exception에 대한 예외가 발생하면 *handleException* 메서드가 모두 처리해준다.</strong></a><br>
그러나 이 예외처리는 선언된 Controller에서만 사용할 수 있다.<br>
그래서 다른 Controller에서 같은 작업을 반복할 수도 있다.



### <a style="color:#00adb5">전역 처리</a>
외부 class로 빼서 <a style="color:red"><strong>@ControllerAdvice</strong></a> annotation을 통해 처리<br>
<a style="color:red"><strong>모든 Controller에서 발생하는 예외를 처리할 수 있다.</strong></a><br>

```java
@ControllerAdvice
public class ExceptionControllerAdvice {

	private Logger logger = LoggerFactory.getLogger(ExceptionControllerAdvice.class);
	
	@ExceptionHandler(Exception.class)
	public String handleException(Exception ex, Model model) {
		logger.error("Exception 발생 : {}", ex.getMessage());
		model.addAttribute("msg", "처리중 에러 발생!!!");
		return "error/error";
	}
	
	@ExceptionHandler(NoHandlerFoundException.class)
	@ResponseStatus(value = HttpStatus.NOT_FOUND)
	public String handle404(NoHandlerFoundException ex, Model model) {
		logger.error("404 발생 : {}", "404 page not found");
		model.addAttribute("msg", "해당 페이지를 찾을 수 없습니다!!!");
		return "error/error";
	}
}
```
<br>
일반적인 Controller 에서는 *@ControllerAdvice* 를 사용하고 Rest에서는 *@RestControllerAdvice* 를 사용한다.<br>
위 코드에서는 Exception ( 최상위 객체 )가 발생하면 handleException 메서드를 실행시킨다.<br><br>

여기서 문제는 <a style="color:red"><strong>404</strong></a>이다. 404 ( 주소 틀렸을 때 ) 는 exception이 아니라 error이다.<br>
*@ResponseStatus(value = HttpStatus.NOT_FOUND)*  이 구문은 404에러 라는 뜻이고<br>
이 에러가 발생하게 되면 web.xml에서 설정해준 것 처럼 에러를 exception으로 받아들여서 <br>
그 exception이 발생 (@ExceptionHandler(NoHandlerFoundException.class) 이 구문 ) 하면 *handle404* 메서드를 실행시킨다.<br>
<br>
간단하게 말하면 <a style="color:red"><strong>handleException 메서드는 400 error 제외 ( 500 error 는 exception이 나서 error가 난 것이다 ) , handle404 메서드는 400 error가 발생했을 때 실행된다.</strong></a><br><br>

Controller 에서의 *@ExceptionHandler* 와 ControllerAdvice 에서의 *@ExceptionHandler* 중 높은 우선순위는 controller 에서의 *@ExceptionHandler* 이다.


<br><br><br><br>
👏 참조<br>
<a href="https://github.com/binghe819/TIL/blob/master/Spring/%EA%B8%B0%ED%83%80/%EC%8A%A4%ED%94%84%EB%A7%81%20%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC%20%EA%B0%9C%EB%85%90%20%EB%B0%8F%20%EC%A0%84%EB%9E%B5.md" target=_blank>https://github.com/binghe819/TIL/blob/master/Spring/%EA%B8%B0%ED%83%80/%EC%8A%A4%ED%94%84%EB%A7%81%20%EC%98%88%EC%99%B8%EC%B2%98%EB%A6%AC%20%EA%B0%9C%EB%85%90%20%EB%B0%8F%20%EC%A0%84%EB%9E%B5.md</a><br>
