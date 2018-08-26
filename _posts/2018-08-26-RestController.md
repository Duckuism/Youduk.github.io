---
layout: post
title: RestController
excerpt: ""
tags: [Boostcourse]
categories: [Spring]
link:
comments: true
pinned: true
image:
  feature: spring.png
---

# 1) RestController란?

**들어가기 전에**

이번 시간엔 Rest API를 Spring MVC를 이용해 작성하려면 어떻게 해야 하는지 방법에 대해 알아보도록 하겠습니다.



------

**학습 목표**

1. Spring MVC에서 제공하는 Rest API를 작성하는 방법에 대해 이해합니다.

------

**핵심 개념**

- Rest API
- Web API
- @RestController
- MessageConvert



RestAPI를 작성하기 위해서 Spring MVC는 @RestController를 제공한다.

 **@RestController**

- Spring 4 에서 Rest API 또는 Web API를 개발하기 위해 등장한 애노테이션합니다.
- 이전 버전(Spring 3)의 @Controller와 @ResponseBody를 포함합니다.



외부에서 전달받은 JSON 메서드를 내부에서 사용할 수 있는 객체로 변환하거나 컨트롤러를 리턴 한 객체가 클라이언트에게 JSON으로 변환해서 전달할 수 있도록 하는 역할을MessageConverter가 수행을 해준다. 이 MessageConverter를 EnableWebMvc로 사용하게 되면 기본으로 제공이 된다.

**MessageConvertor**

- 자바 객체와 HTTP 요청 / 응답 바디를 변환하는 역할
- @ResponseBody, @RequestBody
- @EnableWebMvc 로 인한 기본 설정
- WebMvcConfigurationSupport 를 사용하여 Spring MVC 구현
- Default MessageConvertor 를 제공
- [링크 바로가기](https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java) 의 addDefaultHttpMessageConverters메소드 항목 참조



**MessageConvertor 종류**

아래 처럼 굉장히 다양한 Converter들이 기본으로 제공이 된다.

[![img](https://cphinf.pstatic.net/mooc/20180219_44/1519025088215YszqO_PNG/1.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16773/#)

- **MessageConvertor 종류**



그런데 문제는 json으로 변환을 하기 위해서 기본 MessageConvertor는 jackson 라이브러리를 사용하고 있다. 그래서 만약 jackson 라이브러리가 제대로 추가되어 있지 않으면 JSON을 처리하는 Convertor가 등장하지 않기 때문에 500번 오류를 발생시키게 된다. 그렇기 때문에 반드시 jackson 라이브러리를 추가해줘야 한다.

**JSON 응답하기**

- 컨트롤러의 메소드에서는 JSON으로 변환될 객체를 반환합니다.
- jackson라이브러리를 추가할 경우 객체를 JSON으로 변환하는 메시지 컨버터가 사용되도록 @EnableWebMvc에서 기본으로 설정되어 있습니다.
- jackson라이브러리를 추가하지 않으면 JSON메시지로 변환할 수 없어 500오류가 발생합니다.
- 사용자가 임의의 메시지 컨버터(MessageConverter)를 사용하도록 하려면 WebMvcConfigurerAdapter의 configureMessageConverters메소드를 오버라이딩 하도록 합니다.





------

**생각해보기**

1. Web API에서 JSON메시지를 자주 사용하는 이유는 무엇일까요?
2. JSON메시지의 장점에 대해 찾아보세요.





------

**참고 자료**

[![img](https://cphinf.pstatic.net/mooc/20180219_63/1519025015398PgpAE_PNG/5wN8YGqO2YXAWDQ582wg.png?type=mfullfill_199_148)](https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java)

- **[참고링크] spring-projects/spring-framework**<https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java>


- **[참고링크] Building a RESTful Web Service**<https://spring.io/guides/gs/rest-service/>


- **[참고링크] Building REST services with Spring**<https://spring.io/guides/tutorials/bookmarks/>



# 2) RestController를 이용하여 web api작성하기



**들어가기 전에**

이번 시간엔 Spring MVC를 이용해서 Web API를 직접 작성해 보도록 하겠습니다.

------

**학습 목표**

1. Spring MVC를 이용해 Web API를 작성할 수 있습니다.

------

**핵심 개념**

- @RestController
- @RequestBody
- @PathVariable



예제에서 사용하고 있는 guestbook project에는 이미 jackson라이브러리를 사용하고 있으므로 따로 추가하지 않아도 된다.

**실습코드**

GuestbookApiController.java

```java
package kr.or.connect.guestbook.controller;

import java.util.ArrayList;
import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import kr.or.connect.guestbook.dto.Guestbook;
import kr.or.connect.guestbook.service.GuestbookService;

//RestController를 나타내는 annotation
@RestController
//같은 맵핑으로 여러 요청을 수행한다. 따라서 이 클래스 자체에다가 RequestMappin을 선언하면 안쪽에 있는 것들을 공통으로 사용할 수 있다.
@RequestMapping(path="/guestbooks")
public class GuestbookApiController {
	@Autowired
	GuestbookService guestbookService;
	
    //getMapping되어 있는데 path는 따로 없다? 위에 RequestMapping이 있고 path가 /guestbooks라고 요청이 들어오면서 Content-type이 application/json Get방식으로 들어오면 list 메서드를 실행하게 되는 것.
    //결과값으로는 Map 객체를 반환
    //application/json 요청이기 때문에 DispatcherServlet은 jsonMessageConvert를 내부적으로 사용해서 해당 Map 객체를 json으로 변환해서 전환하게 된다.
	@GetMapping
	public Map<String, Object> list(@RequestParam(name="start", required=false, defaultValue="0") int start) {
		
		List<Guestbook> list = guestbookService.getGuestbooks(start);
		
		int count = guestbookService.getCount();
		int pageCount = count / GuestbookService.LIMIT;
		if(count % GuestbookService.LIMIT > 0)
			pageCount++;
		
		List<Integer> pageStartList = new ArrayList<>();
		for(int i = 0; i < pageCount; i++) {
			pageStartList.add(i * GuestbookService.LIMIT);
		}
		
		Map<String, Object> map = new HashMap<>();
		map.put("list", list);
		map.put("count", count);
		map.put("pageStartList", pageStartList);
		
		return map;
	}
	
    //Geustbook 객체도 json으로 변환되어서 클라이언트한테 갈 것이다.
	@PostMapping
	public Guestbook write(@RequestBody Guestbook guestbook,
						HttpServletRequest request) {
		String clientIp = request.getRemoteAddr();
		// id가 입력된 guestbook이 반환된다.
		Guestbook resultGuestbook = guestbookService.addGuestbook(guestbook, clientIp);
		return resultGuestbook;
	}
	
    //삭제할 id 정보를 담은 pathVariable이 넘어온다.
	@DeleteMapping("/{id}")
	public Map<String, String> delete(@PathVariable(name="id") Long id,
			HttpServletRequest request) {
		String clientIp = request.getRemoteAddr();
		
        //실제 삭제가 되면 1이상의 숫자가 넘어 온다.
		int deleteCount = guestbookService.deleteGuestbook(id, clientIp);
        //삭제된 숫자가 1이상이면 true 아니면 false.
		return Collections.singletonMap("success", deleteCount > 0 ? "true" : "false");
	}
}
```





------

**생각해보기**

1. Web API에게 POST방식으로 값을 전달할 때 JSON메시지를 보냈고, 결과도 JSON메시지를 출력하도록 하였습니다. JSON메시지를 자바객체로 변환하고, 자바객체를 반대로 JSON메시지로 변화하는 부분들이 모두 자동으로 이뤄지고 있는 것을 알 수 있었습니다. 만약 서블릿을 이용해 개발한다면, 이 부분들을 어떻게 구현해야 할까요?
2. 이를 통해 Spring MVC의 장점에 대해 생각해보세요.





------

**참고 자료**

- **[참고링크] Building a RESTful Web Service**<https://spring.io/guides/gs/rest-service/>


- **[참고링크] Building REST services with Spring**<https://spring.io/guides/tutorials/bookmarks/>


