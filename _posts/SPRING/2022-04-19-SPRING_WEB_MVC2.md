---
layout: single
title:  "SPRING_WEB MVC_2"
categories: 
    - SPRING
tags: 
    - [2022-04, WEB, SPRING,]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">SPRING</a>

<center>
<img width="90%" src="./../../images/spring.png">
</center>
<br>

# 📚 <a style="color:#00adb5">Spring MVC</a>

## <a style="color:#00adb5">Controller</a>
@Controller 와 @RequestMapping 선언

### <a style="color:#00adb5">@Controller</a>
<a style="color:red"><strong>Controller Class는 Client의 요청을 처리</strong></a>

```java
@Controller
public class BoardController{

    ...

}
```

- Controller Class를 자동 스캔한다.<br>
    - context:component-scan 선언
    - base-package에 설정된 package 내의 class 중 @Controller 이라는 Annotation이 적용된 클래스는 자동 스캔 대상이 된다.

```xml
<content:component-scan base-package="com.test.board.controller">

-> com.test.board.controller 패키지 안에 @Controller Annotation 이 있으면 자동 스캔한다.
```


### <a style="color:#00adb5">@RequstMapping</a>
- 요청 URL mapping 정보를 설정
- 클래스타입과 메서드에 설정 가능
- value 와 method를 많이 사용한다.
- Client으로부터 요청을 받으면 어떤 Controller에서 어떻게 처리할지 정의하고 나서 <a style="color:red"><strong>그 Controller의 특정 메서드와 매핑하기 위해 Annotation을 사용</strong></a>한다.
- 같은 URL 요청에 대해 HTTP Method ( GET, POST ) 에 따라 서로 다른 메서드를 Mapping 할 수 있다.


```java
@RequestMapping( value = "/board", method = RequestMethod.GET )
public String boardGet(...){
    ...
}

@RequestMapping( value = "/board", method = RequestMethod.POST )
public String boardPost(...){
    ...
}
```

### <a style="color:#00adb5">Controller method의 parameter type</a>

<table>
    <tr>
        <td>Parameter Type</td>
        <td>설명</td>
    </tr>
    <tr>
        <td>HttpServletRequest<br>
            HttpServletResponse<br>
            HttpSession
        </td>
        <td>필요시 Servlet API 를 사용할 수 있음</td>
    </tr>
        <tr>
        <td>Java.util.Locale</td>
        <td>현재 요청에 대한 Locale</td>
    </tr>
        <tr>
        <td>InputStream, Reader</td>
        <td>요청 컨텐츠에 직접 접근할 때 사용</td>
    </tr>
        <tr>
        <td>OutputStream, Writer</td>
        <td>응답 컨텐츠를 생성할 때 사용</td>
    </tr>
        <tr>
        <td><a style="color:red">@PathVariable annotation 적용 파라미터</a></td>
        <td>URI 템플릿 변수에 접근할 때 사용</td>
    </tr>
        <tr>
        <td>@RequestParam annotation 적용 파라미터</td>
        <td>HTTP 요청 파라미터를 매핑<br>
            form에 있는 이름과 다르면 사용해서 이름을 설정해준다.
        </td>
    </tr>
        <tr>
        <td>@RequestHeader annotation 적용 파라미터</td>
        <td>HTTP 요청 헤더를 매핑</td>
    </tr>
        <tr>
        <td>@CookieValue annotation 적용 파라미터</td>
        <td>HTTP 쿠키 매핑</td>
    </tr>
    <tr>
        <td>@RequestBody annotation 적용 파라미터</td>
        <td>HTTP 요청의 body 내용에 접근할 때 사용<br>
            비동기 통신할 때 중요 !!
            </td>
    </tr>
    <tr>
        <td>Map, Model, ModelMap</td>
        <td>View에 전달할 model data를 설정할 때 사용</td>
    </tr>
    <tr>
        <td>커맨드 객체(DTO)</td>
        <td>HTTP 요청 parameter를 저장한 객체<br>
            기본적으로 클래스 이름을 모델명으로 사용<br>
            @ModelAttribute annotation 설정으로 모델명을 설정할 수 있음
            </td>
    </tr>
    <tr>
        <td>Errors, BindingResult</td>
        <td>HTTP 요청 파라미터를 커맨드 객체에 저장한 결과,<br>
        커맨드 객체를 위한 파라미터 바로 다음에 위치
        </td>
    </tr>
    <tr>
        <td>SessionStatus</td>
        <td>폼 처리를 완료했음을 처리하기 위해 사용<br>
        @SessionAttributes annotation을 명시한 session 속성을 제거하도록 이벤트를 발생시킨다.
        </td>
    </tr>
</table>

### <a style="color:#00adb5">@RequstParam annotation 이용한 parameter mapping</a>

```java
// URL 호출 : http://localhost/web/index.do?name=jisoo&age=27

@Controller
public class HomeController{
    @RequestMapping( value = "/index.do", method = RequestMethod.GET)
    public String home(@RequestParam("name" , required = false) String name, @RequestParam("age", defaultValue="25") int age, Model model){
        model.addAttribute("msg", name + "(" + age + ")님 안녕하세요 !!");
        return "index";
    }
}

// required = false :  값이 없어도 null x , false 는 필수적인 것이 아니다
// defaultValue = 25 : 값이 없어도 기본값 25
```

### <a style="color:#00adb5">HTML form과 Command Object ( DTO, VO .. )</a>
Spring MVC는 form에 입력한 data를 JavaBean 객체를 이용해 전송할 수 있다.<br>
<strong>form에서 설정해준 name 값을 가지고 있는 Dto를 호출하면 set 메서드를 자동으로 사용할 수 있게 해준다.</strong>

### <a style="color:#00adb5">View에서 Command 객체에 접근</a>
Command 객체는 자동으로 반환되는 Model에 추가됨<br>
Controller의 @RequestMapping annotation method에서 전달받은 Command 객체에 접근<br>
@ModelAttribute를 사용하여 View에서 사용할 Command 객체의 이름을 변경할 수 있다.





### <a style="color:#00adb5">Controller method의 return type</a>

<table>
    <tr>
        <td>Return Type</td>
        <td>설명</td>
    </tr>
    <tr>
        <td>ModelAndView</td>
        <td>model 정보 및 view 정보를 담고 있는 ModelAndView 객체</td>
    </tr>
    <tr>
        <td>Model</td>
        <td>view에 전달할 객체 정보를 담고 있는 Model을 반환한다.<br>
            이때 이름은 요청 URL로부터 결정된다.<br>
            (RequestToViewNameTranslator)
            </td>
    </tr>    
    <tr>
        <td>Map</td>
        <td>view에 전달할 객체 정보를 담고 있는 Map을 반환한다.<br>
            이때 이름은 요청 URL로부터 결정된다.<br>
            (RequestToViewNameTranslator)
            </td>
    </tr>
    <tr>
        <td>String</td>
        <td>view의 이름을 반환한다.</td>
    </tr>
    <tr>
        <td>View</td>
        <td>view 객체를 직접 리턴, 해당 View 객체를 이용해서 view 를 생성한다.</td>
    </tr>
    <tr>
        <td>void</td>
        <td>method가 ServletResponse나 HttpServletResponse 타입의 parameter를 갖는 경우 method가 직접 응답을 처리한다고 가정한다. 그렇지 않을 경우 요청 URL로부터 결정된 View를 보여준다.<br>
        (RequestToViewNameTranslator)
        </td>
    </tr>
    <tr>
        <td>@ResponseBody Annotation 적용</td>
        <td>method에서 @ResponseBody annotation이 적용된 경우, 리턴 객체를 HTTP 응답으로 전송한다.<br>
            HttpMessageConverter를 이용해서 객체를 HTTP 응답 스트림으로 변환한다.
        </td>
    </tr>