---
layout: single
title:  "REST API_RESTCONTROLLER"
categories: 
    - WEB
tags: 
    - [2022-04, WEB, REST, BACKEND, API]
sidebar:
    nav: "docs"
---

# 📚 <a style="color:#00adb5">REST API</a>

<center>
<img width="90%" src="./../../images/rest.jpg">
</center>
<br>

# 📚 <a style="color:#00adb5">@RestController</a>

## <a style="color:#00adb5">@RestController</a> 란
@RestController 란 <a style="color:red"><strong>@Controller에 @ResponseBody가 추가된 것</strong></a>이다.<br>
주용도는 <a style="color:red"><strong>Json 형태로 객체 데이터를 반환하는 것</strong></a>이다.<br>
최근에 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 객체를 ResponseEntity로 감싸서 반환한다.<br>


## <a style="color:#00adb5">@RestController</a> 예제 코드
<strong>HttpStatus를 설정해주기 위해 ResponseEntity를 사용한다.</strong><br>
ResponseEntity는 Spring Framework에서 제공하는 클래스 중 <a style="color:red"><strong>HttpEntity</strong></a>를 상속받는다.<br>
HttpEntity는 HTTP 요청 ( request ) 또는 응답 ( response ) 에 해당하는 HttpHeader 와 HttpBody를 포함하고 있다.<br>
ResponseEntity는 HttpRequest에 대한 응답 데이터를 포함하는 클래스이다.<br>
따라서 <a style="color:red"><strong>HttpStatus, HttpHeaders, HttpBody</strong></a>를 포함한다.<br>
작동 결과에 따라 응답을 보내줘서 결과를 확인하면 된다.


```java
import java.util.List;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

import com.ssafy.guestbook.model.MemberDto;
import com.ssafy.guestbook.model.service.MemberService;

@RestController
// 밑에 다 @ResponseBody를 쓸거여서 RestController 라고 한다
@RequestMapping("/admin")
@CrossOrigin("*")
public class AdminController {

	private static final Logger logger = LoggerFactory.getLogger(AdminController.class);

	@Autowired
	private MemberService memberService;

	// responseEntity -> 상태코드와 데이터를 같이 묶어서 보낼 수 있다. <반환값 자료형>(반환값, http상태 )
	// HTTPStatus.OK -> 정상적으로 실행됏다
	@GetMapping("/user")
	public ResponseEntity<?> userList() throws Exception {
		List<MemberDto> list = memberService.listMember();

        // 정상적으로 list가 존재하면 list를 반환해주고 상태(OK)를 리턴한다.
        // 존재하지 않으면 상태(NO_CONTENT)를 리턴한다.
		if (list != null && !list.isEmpty()) {
			return new ResponseEntity<List<MemberDto>>(list, HttpStatus.OK);
		} else {
			return new ResponseEntity<Void>(HttpStatus.NO_CONTENT);
		}
	}

    // 등록하기
	@PostMapping("/user")
	public ResponseEntity<?> userRegister(@RequestBody MemberDto memberDto) throws Exception {
		memberService.registerMember(memberDto);
        // listMember 메서드를 호출하고 상태(OK)를 리턴한다.
		return new ResponseEntity<List<MemberDto>>(memberService.listMember(), HttpStatus.OK);
	}


    // id로 회원찾기
	@GetMapping("/user/{userid}")
	public ResponseEntity<?> userInfo(@PathVariable("userid") String userid) throws Exception {
		MemberDto memberDto = memberService.getMember(userid);
        // 정상적으로 memberDto가 존재하면 memberDto를 반환해주고 상태(OK)를 리턴한다.
        // 존재하지 않으면 상태(NO_CONTENT)를 리턴한다.
		if (memberDto != null) {
			return new ResponseEntity<MemberDto>(memberDto, HttpStatus.OK);
		} else {
			return new ResponseEntity<Void>(HttpStatus.NO_CONTENT);
		}
	}

    // update
	@PutMapping("/user")
	public ResponseEntity<?> userModify(@RequestBody MemberDto memberDto) throws Exception {
		memberService.updateMember(memberDto);
        // listMember 메서드를 호출하고 상태(OK)를 리턴한다.
		return new ResponseEntity<List<MemberDto>>(memberService.listMember(), HttpStatus.OK);
	}

    // delete
	@DeleteMapping("/user/{userid}")
	public ResponseEntity<?> userDelete(@PathVariable("userid") String userid) throws Exception {
		memberService.deleteMember(userid);
        // listMember 메서드를 호출하고 상태(OK)를 리턴한다.
		return new ResponseEntity<List<MemberDto>>(memberService.listMember(), HttpStatus.OK);
	}
}
```