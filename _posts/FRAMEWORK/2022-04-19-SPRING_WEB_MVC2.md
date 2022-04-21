---
layout: single
title:  "SPRING_WEB MVC_2"
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

# 📚 <a style="color:#00adb5">Spring MVC</a>

## <a style="color:#00adb5">Controller</a>
<a style="color:red"><strong>@Controller 와 @RequestMapping 선언</strong></a><br>
method 단위의 mapping이 가능


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
request에 저장되는 command 객체의 이름은 첫글자를 소문자로 변경한 것이다 ( ex, BoardDto -> boardDto )
@ModelAttribute를 사용하여 View에서 사용할 Command 객체의 이름을 변경할 수 있다.<br>

```java
@Controller
@RequestMapping("/board")
public class BoardController{

    @RequestMapping(value="/write.do", method = RequestMethod.POST)
    public String write( @ModelAttribute("article") BoardDto boardDto ){
        return "board/writeok";
    }
}

/*
-> writeok.jsp 에서는 
-----
제목 : ${article.subject}<br>
내용 : ${article.content}
-----
으로 사용된다.
만약 ModelAttribute를 사용하지 않는다면 article -> boardDto를 사용한다.
*/

```

### <a style="color:#00adb5">@CookieValue annotation을 이용한 Cookie mapping</a>
@CookieValue annotation을 이용한 Cookie mapping

```java
@Controller
public class HomeController{

    public String hello(@CookieValue(value="author", requires=false, defalutValue="user") String authorValue){
        return "ok";
    }
}
```


### <a style="color:#00adb5">@RequestBody</a>





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
</table>



## <a style="color:#00adb5">View</a>
<a style="color:red"><strong>Controller에서는 처리 결과를 보여줄 View 이름이나 객체를 리턴하고, DispatcherServlet은 View 이름이나 View 객체를 이용하여 view 생성</strong></a><br>

### <a style="color:#00adb5">ViewResolver</a>
<a style="color:red"><strong>논리적 view와 실제 JSP파일 mapping</strong></a><br>

InternalResourceViewResolver는 <a style="color:red"><strong>prefix + 논리뷰 + suffix</strong></a>로 설정<br>
-> /WEB-INF/views/board.jsp<br><br>

servlet-context.xml

```xml
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>
```

### <a style="color:#00adb5">View</a> 이름 명시적 지정
ModelAndView와 String 리턴 타입

```java
1. 
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public ModelAndView hello(){
        ModelAndView mav = new ModelAndView("hello");
        return mav;
    }
}

2.
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public ModelAndView hello(){
        ModelAndView mav = new ModelAndView();
        mav.setViewName("hello");
        return mav;
    }
}

3.
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public String hello(){
        return "hello";
    }
}

```

### <a style="color:#00adb5">View</a> 이름 자동 지정
RequestToViewNameTranslator를 이용하여 URL로 부터 view 이름을 결정<br>
자동지정 유형<br>
- return type이 Model이나 Map인 경우
- return type이 void이면서 ServletResponse나 HttpServletResponse 타입의 parameter가 없는 경우

```java
@Controller
public class HomeController{
    
    @RequestMapping("/hello.do")
    public Map<String, Object> hello(){
        Map<String, Object> model = new HashMap<String, Object>();
        return model;
    }
}

-> return type이 Map 이므로 hello가 view 이름이 된다.
-> 크게 권장하지는 않는다.
```


### <a style="color:#00adb5">redirect view</a>
Spring Framework는 기본적으로 페이지로 forward 된다.<br>
이 때 redirect로 넘겨주고 싶을 때 사용<br>
View 이름에 <a style="color:red"><strong>"redirect:" 접두어를 붙이면</strong></a> 지정한 페이지로 redirct 된다.

```java
@Controller
public class BoardRegisterController{
    @Autowired
    private BoardService boardService;

    @RequestMapping( value = "board/register.html", method=RequestMethod.POST)
    public String register(@ModelAttribute("article") BoardDto boardDto) {
        boardService.registerArticle(boardDto);
        return "redirect:board/list.html?pg=1";
    }
}
```


## <a style="color:#00adb5">Model</a>
<a style="color:red"><strong>View에 전달하는 데이터</strong></a>
- @RequestMapping annotation이 적용된 method의 *Map, Model, ModelMap*
- @RequestMapping method가 return하는 *ModelAndView*
- @ModelAttribute annotation이 적용된 method가 *return 한 객체*

### <a style="color:#00adb5">method의 argument로 받는 방식 ( Map, Model, ModelMap )</a>

```java
1. Map
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public String hello(Map model){
        model.put("msg". "hi");
        return "hello";
    }
}

2. Model
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public String hello(Model model){
        model.addAttribute("msg". "hi");
        return "hello";
    }
}

3. ModelMap
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public String hello(ModelMap model){
        model.addAttribute("msg". "hi");
        return "hello";
    }
}

```

### <a style="color:#00adb5">Model 생성 - Model Interface 주요 method</a>
- Model addAttribute(String name, Object value);
- Model addAttribute(Object value);
- Model addAllAttributes(Collection<?> values);
- Model addAllAttributes(Map<String, ?> attributes);
- Model mergeAttributes(Map<String, ?> attributes);
- boolean containsAttribute(String name);


### <a style="color:#00adb5">ModelAndView를 통한 Model 설정</a>
- Controller에서 처리결과를 보여줄 view 와 view에 전달할 값 ( model )을 저장하는 용도로 사용
- setViewName(String viewname);
- addObject(String name, Object value);
<br>

MAV 는 addObject 이다 !!<br>
Model 생성은 addAttribute 이다 !!

```java
@Controller
public class HomeController{

    @RequestMapping("/hello.do")
    public ModelAndView hello(){
        ModelAndView mav = new ModelAndView();
        mav.setViewName("hello");
        mav.addObject("msg","안녕하세요);
        return mav;
    }
}
```


### <a style="color:#00adb5">@ModelAttribute를 이용한 model data 처리</a>
@RequestMapping annotation이 적용되지 않은 별도 method로 모델이 추가될 객체를 생성한다.<br>
주로 공통으로 보내주는 구문에 많이 사용한다.<br>

```java

@ModelAttribute("modelMsg")
public String msg(){
    return "bye";
}

-> ${modelMsg} 로 불러주면 bye가 출력된다.
```
