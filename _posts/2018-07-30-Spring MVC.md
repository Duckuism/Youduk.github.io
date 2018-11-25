---
layout: post
title: Spring MVC
excerpt: ""
tags: [Boostcourse]
categories: [Spring]
link:
comments: true
pinned: true
image:
  feature: spring.png
---

# 1) Spring MVC란?

**들어가기 전에**

이번 시간엔 Spring 프레임워크에서 웹 어플리케이션 작성을 위해 제공하는 Web MVC모듈에 대해 알아보도록 하겠습니다.

------

**학습 목표**

1. MVC Model 1과 MVC Model 2 구조의 차이점에 대해 이해합니다.
2. 발전된 형태의 MVC Model2 구조에 대해 이해합니다.

------

**핵심 개념**

- MVC Model 1
- MVC Model 2
- Spring MVC

**MVC란?**

- MVC는 Model-View-Controller의 약자입니다.
- 원래는 제록스 연구소에서 일하던 트뤼그베 린즈커그가 처음으로 소개한 개념으로, 데스트톱 어플리케이션용으로 고안되었습니다. 이 개념을 웹 애플리케이션이나 다른 곳에서도 사용을 하게 된 것이다.
- Model : 모델은 뷰가 렌더링하는데 필요한 데이터입니다. 예를 들어 사용자가 요청한 상품 목록이나, 주문 내역이 이에 해당합니다.
- View : 웹 애플리케이션에서 뷰(View)는 실제로 보이는 부분이며, 모델을 사용해 렌더링을 합니다. 뷰는 JSP, JSF, PDF, XML등으로 결과를 표현합니다.
- Controller : 컨트롤러는 사용자의 액션에 응답하는 컴포넌트입니다. 컨트롤러는 모델을 업데이트하고, 다른 액션을 수행합니다.

[![img](https://cphinf.pstatic.net/mooc/20180219_180/1519003368125BcfqV_PNG/1.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16762/#)

- **MVC Model 1 아키텍처**

  1. 브라우저가 요청을 하게되면 해당 요청을 JSP가 받는다. 따라서 요청만큼 JSP 페이지가 존재해야한다. 
  2. 요청을 받은 JSP는 Java로 만들어진 클래스인 Java bean(JDBC로 작성했던 Role Dao)을 이용해서 데이터베이스를 사용한다.
  3. 그리고 이 결과를 화면에 출력한다.

  이 방식의 문제점은 JSP 자체에 Java 코드랑 HTML 코드들이 섞여있다는 것이다. 그렇다보니 유지보수가 굉장히 어려웠다. 그래서 이 방식을 해결하게 위해 나온 것이 MVC Model2 아키텍쳐이다.


[![img](https://cphinf.pstatic.net/mooc/20180219_65/1519003382079lUcI5_PNG/2.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16762/#)

- **MVC Model 2 아키텍처**

  1. 요청 자체를 서블릿이 받는다. (서블릿이 Controller의 역할)
  2. 서블릿이 Java bean을 이용해서 DB에서 데이터를 꺼내오고 (Java bean이 Model 역할)
  3. 결과를 JSP를 통해서 화면에 보여준다. (JSP가 View의 역할)


[![img](https://cphinf.pstatic.net/mooc/20180219_149/15190034013354diDI_PNG/3.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16762/#)

- **MVC Model2 발전형태**

  1. 서블릿은 관련 요청을 처리하기에 불편한 구조이다. 이런 단점을 해결하기 위해서 클라이언트가 보내는 모든 요청을 단 하나만 존재하는 프론트 컨트롤러라고 하는 서블릿 클래스가 다 받는다. 이 프론트 컨트롤러는 요청만 받고 실제 일은 처리하지 않는다. 실제 일은 컨트롤러 클래스(핸들러 클래스)에게 위임한다. 이렇게 함으로써 관련된 URL을 하나의 클래스에서 다 처리할 수 있도록 하게 된다.
  2. 컨트롤러 클래스(핸들러 클래스)는 Java bean등을 이용해서 결과를 만들어내고, 이 결과를 모델에 담아 프론트 컨트롤러에게 보낸다.
  3. 프론트 컨트롤러는 알맞는 뷰에게 모델을 전달해서 그 결과를 출력하게 된다.


[![img](https://cphinf.pstatic.net/mooc/20180219_73/1519003417760TqmnB_PNG/4.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16762/#)

- **Spring Web Module**

  Model2 MVC 패턴을 지원하는 Spring Module 

  앞에서 얘기한 MVC Model2의 발전 형태가 Spring 모듈 중 하나인 Web Module로 구현이 되어있고, 이러한 웹 모듈은 Spring MVC라고 한다.

 

------

**생각해보기**

1. 프론트 컨트롤러(Front Controller)는 모든 요청을 받아 들여 공통적인 작업을 처리해 줍니다. 이를 통해 얻을 수 있는 장점엔 어떤 것이 있을 수 있을까요?

 

 

------

**참고 자료**

- **[참고링크] Web MVC framework**<https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/html/mvc.html>


- **[참고링크] MVC Model2 | Opendocs**<https://myblog.opendocs.co.kr/archives/tag/mvc-model2>


- **[참고링크] Model 1 and Model 2 (MVC) Architecture**<https://www.javatpoint.com/model-1-and-model-2-mvc-architecture>


- **[참고링크] Modules**<https://docs.spring.io/spring/docs/3.0.0.M4/reference/html/ch01s02.html>


- **[참고링크] IBM Knowledge Center**<https://www.ibm.com/support/knowledgecenter/SSRTLW_9.1.1/com.ibm.etools.struts.doc/topics/cstrdoc001.html>



# 2) Spring MVC구성요소

**들어가기 전에**

이번 시간엔 Spring MVC에서 가장 핵심적인 역할을 수행하는 DispacherServlet이 어떤 순서로 동작하는지 살펴보도록 하겠습니다.

이를 통해서 Spring MVC에서 사용되는 컴포넌트들에 대해 알아보도록 하겠습니다.

------

**학습 목표**

1. DispacherServlet이 어떤 순서로 동작하는지 이해한다.
2. DispacherServlet에서 사용되는 컴포넌트(객체)들이 어떤 것들이 있는지 안다.

------

**핵심 개념**

- DispacherServlet
- HandlerMapping
- HandlerAdpater
- ViewResolver



**Spring MVC 기본 동작 흐름**

[![img](https://cphinf.pstatic.net/mooc/20180219_116/1519003779294ejdEx_PNG/1.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **Spring MVC 기본 동작 흐름**
  - Spring MVC는 Model2 아키텍쳐로 구성이 되어있다고 했다.
  - Database를 제외한 파란색 부분들은 모두 Spring MVC가 제공해주는 것들이다.
  - 개발자가 만들어야하는 부분들은 보라색으로 되어있는 부분들이다.
  - 녹색인 View는 스프링이 제공해주는 부분도 있고 개발자가 만들어야하는 부분도 같이 존재한다고 보면 된다.
  - 동작 흐름 설명
    1. 클라이언트가 요청을 보내면 보낸 모든 요청을 Dispatcher Servlet 클래스가 받는다. 
    2. Dispatcher Servlet은 받은 요청을 처리해 줄 컨트롤러와 메서드가 무엇인지 Handler Mapping에게 물어본다.
       1. Handler Mapping이 혼자서 결정해서 연결할 수는 없다. 이 부분은 개발자가 Spring MVC로 개발하면 어떤 요청에 어떤 컨트롤러가 동작할지를 xml파일이나 java파일에 어노테이션으로 설정을 하게 된다. 이런 정보들을 Spring으로 만들어진 웹 어플리케이션이 실행할 때 Handler Mapping 객체들이 생성이 되면서 관리를 하게 되는 것이다.
    3. Handler Adapter에게 실행을 요청한다. 
    4. 2번에서 결정된 컨트롤러와 해당 메서드가 실행이 된다.
    5. 4번의 결과를 Model에 받아서 Dispatcher Servlet에 전달을 한다. 이 때 Dispatcher Servlet은 컨트롤러가 반환한 view name을 알아오게 될 것이다.
    6. 컨트롤러가 리턴한 view name을 가지고 적절한 View Resolver를 통해서 뷰를 출력하게 된다. View Resolver가 어떤 View인지에 대한 정보를 알려주게 되면
    7. Dispatcher Servlet은 해당 View 접근해서
    8. 접근한 View로 응답을 하게 된다.



SpringMVC를 이해한다는 것은 DispatcherServlet이 어떻게 동작하는지 이해하는 것이라고 말할 수 있다. DispathcerServlet이 요청을 받아서 결과를 출력하기까지 지금 아래에 기술되어 있는 여러가지 컴포넌트를 사용하게 될 것이다.

* DispatcherServlet
  * HandlerMapping
  * HandlerAdapter
  * MultipartResolver
  * LocaleResolver
  * ThemeResolver
  * HandlerExceptionResolver
  * RequestToViewNameTranslator
  * ViewResolver
  * FlashMapManager



**DispatcherServlet**

- DispatcherServlet을 프론트 컨트롤러 (Front Controller)라고 부른다. (회사 대표번호 느낌)
- 클라이언트의 모든 요청을 받은 후 이를 처리할 핸들러에게 넘기고 핸들러가 처리한 결과를 받아 사용자에게 응답 결과를 보여준다.
- DispathcerServlet은 여러 컴포넌트를 이용해 작업을 처리한다.

[![img](https://cphinf.pstatic.net/mooc/20180219_281/1519003870301bOehw_PNG/2.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름**

  - DispatcherServlet에 이런 식으로 코드가 만들어져 있겠구나라고 유추할 수 있다.


[![img](https://cphinf.pstatic.net/mooc/20180219_91/1519003885824QT31y_PNG/3.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 요청 선처리 작업**

  - Locale결정: SpringMVC는 지역화를 지원한다. 지역화 처리를 위해 브라우저 헤더 정보의 언어 설정 정보에 따라 Locale결정.
  - RequestContextHolder에 요청 저장 : 이 부분은 스레드(프로그램 내, 프로세스 내에서 실행되는 흐름의 단위) 로컬 객체이다. 요청을 받아서 응답할 때까지 HttpServletRequest, HttpServletResponse등을 Spring이 관리하는 객체 안에서 사용할 수 있도록 해주는 것들을 이야기한다. 나중에 SpringMVC 사용 도중 컨트롤러가 가진 메서드 안에서 Request 객체가 필요하다면 인자에다가 HttpServletRequest reqeust라고 선언만 하면 해당 메서드 안에서 request를 쓸 수 있다. 이런 방식은 Spring이 웹 기술에 종속되는 문제를 가지기도 한다. 따라서 아주 권장하는 방법은 아니다.
  - FlashMap복원 : Spring 3에서 추가된 기능. FlashMap은 Redirect로 값을 전달할 때 사용된다. Redirect로 값을 전달할 때 우리는 ?, 파라미터와 같은 것들을 이용한다. 그런데 이렇게 작업하다보면 URL이 굉장히 복잡해진다. 이런 부분때문에 FlashMap을 사용하는데, FlashMap을 사용하면 Redirect될 때 딱 한 번 값을 유지시킬 수 있게 해주는 것을 이야기한다.
  - 사용자가 파일 업로드를 했을 때 파일 정보를 읽어들이는 특수한 형태의 Request객체가 필요하다. 이 특수한 Request 객체를 사용할 때 멀티 파트라는 요청이 들어오게 되면 Request를 MultipartResolver가 어떤 멀티 파트를 사용할 지 결정한다. 그리고 실제 요청을 처리하는 핸들러를 결정하고 실행을 하는 역할까지 해주는 것이 선처리작업에서 하는 일이다.


**요청 선처리 작업시 사용된 컴포넌트**

org.springframework.web.servlet.LocaleResolver

- 지역 정보를 결정해주는 전략 오브젝트이다.
- 디폴트인 AcceptHeaderLocalResolver는 HTTP 헤더의 정보를 보고 지역정보를 설정해준다.

org.springframework.web.servlet.FlashMapManager

- FlashMap객체를 조회(retrieve) & 저장을 위한 인터페이스
- RedirectAttributes의 addFlashAttribute메소드를 이용해서 저장한다.
- 리다이렉트 후 조회를 하면 바로 정보는 삭제된다.

org.springframework.web.context.request.RequestContextHolder

- 일반 빈에서 HttpServletRequest, HttpServletResponse, HttpSession 등을 사용할 수 있도록 한다.
- 해당 객체를 일반 빈에서 사용하게 되면, Web에 종속적이 될 수 있다.

org.springframework.web.multipart.MultipartResolver

- 멀티파트 파일 업로드를 처리하는 전략



[![img](https://cphinf.pstatic.net/mooc/20180219_20/1519003954110F9wyd_PNG/4.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 요청 전달**


**요청 전달시 사용된 컴포넌트**

org.springframework.web.servlet.HandlerMapping

- HandlerMapping구현체는 어떤 핸들러가 요청을 처리할지에 대한 정보를 알고 있다.
- 디폴트로 설정되는 있는 핸들러매핑은 BeanNameHandlerMapping과 DefaultAnnotationHandlerMapping 2가지가 설정되어 있다.

org.springframework.web.servlet.HandlerExecutionChain

- HandlerExecutionChain구현체는 실제로 호출된 핸들러에 대한 참조를 가지고 있다.
- 즉, 무엇이 실행되어야 될지 알고 있는 객체라고 말할 수 있으며, 핸들러 실행전과 실행후에 수행될 HandlerInterceptor도 참조하고 있다.

org.springframework.web.servlet.HandlerAdapter

- 실제 핸들러를 실행하는 역할을 담당한다.
- 핸들러 어댑터는 선택된 핸들러를 실행하는 방법과 응답을 ModelAndView로 변화하는 방법에 대해 알고 있다.
- 디폴트로 설정되어 있는 핸들러어댑터는 HttpRequestHandlerAdapter, SimpleControllerHandlerAdapter, AnnotationMethodHanlderAdapter 3가지이다.
- @RequestMapping과 @Controller 애노테이션을 통해 정의되는 컨트롤러의 경우 DefaultAnnotationHandlerMapping에 의해 핸들러가 결정되고, 그에 대응되는 AnnotationMethodHandlerAdapter에 의해 호출이 일어난다.



[![img](https://cphinf.pstatic.net/mooc/20180219_167/1519004040926yL8eC_PNG/5.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 요청 처리**

인터셉터는 '필터'라고 생각하면 편하다.

**요청 처리시 사용된 컴포넌트**

org.springframework.web.servlet.ModelAndView

- ModelAndView는 Controller의 처리 결과를 보여줄 view와 view에서 사용할 값을 전달하는 클래스이다.



[![img](https://cphinf.pstatic.net/mooc/20180219_26/1519004078279fGdRP_PNG/6.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 예외처리**


**예외 처리시 사용된 컴포넌트**

org.springframework.web.servlet.handlerexceptionresolver

- 기본적으로 DispatcherServlet이 DefaultHandlerExceptionResolver를 등록한다.
- HandlerExceptionResolver는 예외가 던져졌을 때 어떤 핸들러를 실행할 것인지에 대한 정보를 제공한다.





[![img](https://cphinf.pstatic.net/mooc/20180219_66/1519004113425TanBR_PNG/7.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 뷰 렌더링 과정**


**뷰 렌더링 과정시 사용된 컴포넌트**

org.springframework.web.servlet.ViewResolver

- 컨트롤러가 리턴한 뷰 이름을 참고해서 적절한 뷰 오브젝트를 찾아주는 로직을 가진 전략 오프젝트이다.
- 뷰의 종류에 따라 적절한 뷰 리졸버를 추가로 설정해줄 수 있다.





[![img](https://cphinf.pstatic.net/mooc/20180219_296/1519004150778ofOPV_PNG/8.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16763/#)

- **DispatcherServlet 내부 동작흐름 상세 - 요청 처리 종료**

------

**생각해보기**

1. DispacherServlet은 요청을 받은 후, 요청을 처리하기 위해서 여러가지 작업을 수행하고 있습니다. 
2. 개발자는 DispacherServlet이 어떤 방식으로 동작하는지 이해한다면 좀 더 잘 Spring MVC를 잘 사용할 수 있습니다.
3. Spring외에 다른 프레임워크를 학습할 때에도, 해당 프레임워크의 동작원리를 이해하는 것은 굉장히 중요합니다.
4. 어떻게 하면, 다른 사람이 만든 라이브러리나 프레임워크를 좀 더 잘 이해할 수 있을지 고민해보세요.

------

**참고 자료**

- **[참고링크] Overview of Spring MVC Architecture**<https://terasolunaorg.github.io/guideline/1.0.1.RELEASE/en/Overview/SpringMVCOverview.html>


- **[참고링크] Modules**<https://docs.spring.io/spring/docs/3.0.0.M4/reference/html/ch01s02.html>


- **[참고링크] Spring MVC - DispatcherServlet 동작 원리 출처: https://jess-m.tistory.com/15 [Jess's Home]**<https://jess-m.tistory.com/15>


- **[참고링크] Spring DispatcherServlet의 기본 7가지 DI전략**<https://kimddochi.tistory.com/86>


[![img](https://cphinf.pstatic.net/mooc/20180219_261/151900438006802DCv_JPEG/pEJs3PgwjklDD5acHu7a.jpg?type=mfullfill_199_148)](https://samerabdelkafi.wordpress.com/2014/08/03/spring-mvc-full-java-based-config/)

- **[참고링크] Spring MVC – Full java based config**<https://samerabdelkafi.wordpress.com/2014/08/03/spring-mvc-full-java-based-config/>


- **[참고링크] web.xml vs Initializer with Spring**<https://www.baeldung.com/spring-xml-vs-java-config>


- **[참고링크] Spring – Mixing XML and JavaConfig**<https://www.mkyong.com/spring/spring-mixing-xml-and-javaconfig/>


[![img](https://cphinf.pstatic.net/mooc/20180219_37/1519004424262VcnFy_JPEG/FYpOX6DaSR44ofFn7Wx6.jpg?type=mfullfill_199_148)](https://github.com/arey/spring-javaconfig-sample/blob/master/src/main/webapp/WEB-INF/web.xml)

- **[참고링크] arey/spring-javaconfig-sample**<https://github.com/arey/spring-javaconfig-sample/blob/master/src/main/webapp/WEB-INF/web.xml>


- **[참고링크] WebMvcConfigurationSupport**<https://docs.spring.io/spring/docs/3.0.6.RELEASE_to_3.1.0.BUILD-SNAPSHOT/3.1.0.BUILD-SNAPSHOT/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.html>


- **[참고링크] Spring mvc (2) 그리고 Spring boot**<https://wonwoo.ml/index.php/post/1590>


- **[참고링크] Migrate Spring MVC servlet.xml to Java Config**<https://www.luckyryan.com/2013/02/07/migrate-spring-mvc-servlet-xml-to-java-config/>


- **[참고링크] Spring RequestMapping**<https://www.baeldung.com/spring-requestmapping>



# 3) Spring MVC를 이용한 웹 페이지 작성 실습

**들어가기 전에**

이번 시간엔 Spring MVC를 이용하여 웹 어플리케이션을 작성하는 방법에 대하여 실습을 통해 알아보도록 하겠습니다.

------

**학습 목표**

- Spring MVC를 이용해 프로젝트를 구성할 수 있고, 개발자가 작성해야 할 파일이 무엇인지 이해한다.
- Spring MVC를 이용해 웹 어플리케이션을 작성할 수 있다.

------

**핵심 개념**

- DispacherServlet
- WebApplicationInitializer
- @RequestMapping = @GetMapping = @PostMapping

 

**DispatcherServlet을 FrontController로 설정하기**

DispatcherServlet이 FrontController의 역할을 한다고 하였으나,  DispatcherServlet이 FrontController라는 설정을 해주지 않는다면, 제대로 역할을 할 수가 없다. 따라서 꼭 설정을 해주어야한다.

- web.xml 파일에 설정
  - DispatcherServlet도 서블릿이기 떄문에 web.xml 파일에다가 설정할 수가 있다
  - 서블릿을 학습할 때, 서블릿을 하나 생성하면 servlet과 servlet mapping이라는 xml태그에다가 각각의 값들을 넣어줘서 설정해줬었다. 이 부분을 조금만 활용하면 Spring이 제공하는 DispatcherServlet을 FrontController의 역할을 할 수 있도록 설정을 할 수가 있다.
- ~~javax.servlet.ServletContainerInitializer 사용~~( 사용 빈도가 낮은 방법이므로 강의에서는 다루지 않음.)
  ~~\- 서블릿 3.0 스펙 이상에서 web.xml파일을 대신해서 사용할 수 있다.~~
- org.springframework.web.WebApplicationInitializer 인터페이스를 구현해서 사용

**web.xml파일에서 DispatcherServlet 설정하기 1/2**

[![img](https://cphinf.pstatic.net/mooc/20180219_194/151900563324539bbk_PNG/1.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16764/#)

- **xml spring 설정 읽어들이도록 DispathcerServlet설정**
  - servlet-name은 servlet mapping이 갖고 있는 servlet-name하고 일치하기만 하면 된다. servlet-class가 실제로 내가 동작시킬 클래스를 의미하는 것이다. 이 때는 Spring이 제공하고 있는 DispatcherServlet을 이용할 것이기 때문에 반드시 패키지 명을 포함해서 Spring이 제공하고 있는 클래스 명을 제대로 넣어주어야한다. init-param에서는 DispatcherServlet같은 경우는 Spring이 제공하고 있기 때문에 실제로 내가 무슨 일을 하고 싶은지에 대한 내용까지는 알 수 없을 것이다. 그런 것에 대한 설정을 하고 있는 것이 init-param에 지정을 하는 부분이다. param-value에 입력된 xml파일에다가 실제로 우리가 어떤 일들을 할 것인지 알려주는 것이다.

[![img](https://cphinf.pstatic.net/mooc/20180219_25/1519005657037r4xE4_PNG/2.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16764/#)

- **Java config spring 설정 읽어들이도록 DispathcerServlet설정**
  - Dispatcher Servlet이 xml파일이 아니라 java config를 이용해서 사용을 할 수 있게 하는 방법이다. 따라서 init-param에 xml파일이 아니라 자바 클래스명을 넣고 있는 것을 확인할 수 있다. 이 부분은 자바 config 파일을 읽어오고 있다고 기억을 하면 된다. 이 방법으로 수업 실습을 진행한다.
  - 요청이 들어오면 서블릿이었을 경우에 url-pattern에 우리가 원하는 URL 주소를 넣고 이 URL 요청이 들어오면 실제 servlet-name과 같은 name으로 매핑되어있는 servlet-class가 실행한다. 위에서는 url-pattern이 '/'라고 설정이 되어있는데, 이렇게 설정이 되어있으면 어떤 특정한 하나의 요청만 받아들이는 것이 아니라 모든 요청을 받게 된다. 즉, 모든 요청을 DispatcherServlet이 받도록 설정한 것이다.

**WebApplicationInitializer를 구현해서 설정하기 1/2**

이 방법의 단점은 처음 웹 어플리케이션이 구동되는 시간이 오래 걸릴 수 있다는 것이다. Spring MVC는 WebApplicationInitializer인터페이스를 구현한 구현체를 찾고 해당 객체의 onStartup메서드를 이용해서 초기화를 하기 때문이다.

- Spring MVC는 ServletContainerInitializer를 구현하고 있는 SpringServletContainerInitializer를 제공한다.
- SpringServletContainerInitializer는 WebApplicationInitializer 구현체를 찾아 인스턴스를 만들고 해당 인스턴스의 onStartup 메소드를 호출하여 초기화한다.

[![img](https://cphinf.pstatic.net/mooc/20180219_225/15190057369849AXoR_PNG/3.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16764/#)

- **WebApplicationInitializer를 구현해서 설정하기 2/2**
  - 수업에서 사용하지는 않고 이렇게 사용할 수도 있다는 것을 설명하기 위한 목적이다.

**Spring MVC 설정**

DispatcherServlet에 대한 설정은 web.xml에서 하고 DispatcherServlet이 읽어들여야 될 설정은 별도로 하게 된다. 우리는 이런 설정을 자바 config로 한다고 했었다. DispatcherServlet은 해당 설정 파일을 읽어들여서 내부적으로 Spring 컨테이너인 ApplicationContext를 생성하게 되는 것이다.

- kr.or.connect.webmvc.config.WebMvcContextConfiguration

[![img](https://cphinf.pstatic.net/mooc/20180219_209/1519005776948gyaN4_PNG/4.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16764/#)

- **Spring MVC 설정**



위에서 사용한 어노테이션을 자세히 살펴보면,

**@Configuration**

* 이 애노테이션으로 인해 자바 config파일이라는 것을 알 수 있게 해준다.

- org.springframework.context.annotation의 Configuration 애노테이션과 Bean 애노테이션 코드를 이용하여 스프링 컨테이너에 새 로운 빈 객체를 제공할 수 있다.

**@EnableWebMvc**

- DispatcherServlet의 RequestMappingHandlerMapping, RequestMappingHandlerAdapter, ExceptionHandlerExceptionResolver, MessageConverter 등 Web에 필요한 빈(bean)들을 대부분 자동으로 설정해준다.
- xml로 설정의 <mvc:annotation-driven/> 와 동일하다. 만약 자바 config가 아니라 xml파일로 설정했다면 mvc:annotation-driven같은 태그가 해당 역할을 대신해줄 것이다. 
- 기본 설정 이외의 설정이 필요하다면 WebMvcConfigurerAdapter 를 상속받도록 Java config class를 작성한 후, 필요한 메소드를 오버라이딩 하도록 한다.

[![img](https://cphinf.pstatic.net/mooc/20180219_11/1519005866922qyYP8_PNG/5.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16764/#)

- **@EnableWebMVC**에 대한 소스 코드
  - 위의 소스 코드를 살펴 보면 DelegatingWebMvcConfiguration을 import하고 있다.
  - 그리고 DelegatingWebMvcConfiguration 클래스는 WebMvcConfigurationSupport를 상속받고 있는 것을 볼 수 있다.
  - WebMvcConfigurationSupport의 소스를 좀 찾아보면 어떤 객체들이 기본으로 설정이 되어 있는지 조금 더 자세히 알 수 있을 것이다.


**WebMvcConfigurationSupport**

- <https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java>
- WebMvcConfigurationSupport 클래스가 구현되어있는 소스 코드를 볼 수 있다.

 

**@ComponentScan**

* Spring MVC에서는 핸들러, 즉 Controller를 찾아야 한다. 컨트롤러를 찾기 위해서는 ComponentScan 애노테이션을 사용한다. 우리가 직접 만든 bean(class)을 사용하려면 xml파일에다가 bean element를 이용해서 직접 등록하거나 애노테이션을 이용한다. 이 때 사용하는 Controller, Service, Repository, Component등의 애노테이션이 붙은 클래스를 찾아서 스프링 컨테이너가 관리하게 해주는 애노테이션이 바로 ComponentScan이다.

- ComponentScan애노테이션을 이용하면 Controller, Service, Repository, Component애노테이션이 붙은 클래스를 찾아 스프링 컨테이너가 관리하게 된다.
- 우리가 작성할 컨트롤러에는 URL Mapping 정보가 애노테이션으로 설정이 되어 있을 것이다. 이런 URL Mapping 정보는 DispatcherServlet이 관리하는 RequestMapping 객체들로 설정이 될 것이고 이것을 위해서 DefaultAnnotationHandlerMapping과 RequestMappingHandlerMapping의 구현체가 사용이 될 것이다. 
- DefaultAnnotationHandlerMapping과 RequestMappingHandlerMapping구현체는 다른 핸드러 매핑보다 훨씬 더 정교한 작업을 수행한다. 이 두 개의 구현체는 애노테이션을 사용해 매핑 관계를 찾는 매우 강력한 기능을 가지고 있다. 이들 구현체는 스프링 컨테이너 즉 애플리케이션 컨텍스트에 있는 요청 처리 빈에서 RequestMapping애노테이션을 클래스나 메소드에서 찾아 HandlerMapping객체를 생성하게 된다.
  - HandlerMapping은 서버로 들어온 요청을 어느 핸들러로 전달할지 결정하는 역할을 수행한다.
- DefaultAnnotationHandlerMapping은 DispatcherServlet이 기본으로 등록하는 기본 핸들러 맵핑 객체이고, RequestMappingHandlerMapping은 더 강력하고 유연하지만 사용하려면 명시적으로 설정해야 한다.
- ComponentScan할 때 반드시 basePackages는 지정을 해 주어야한다. 그렇지 않으면 어느 패키지부터 찾아내야 될 지를 몰라서 제대로 수행이 안 된다. basePackages를 사용하고 중괄호를 사용하게 되면 패키지가 여러 개 있었을 때 콤마(,)를 사용해서 지정을 할 수가 있고, 중괄호 없이 사용하면 해당 패키지 하나만 사용하면 된다. 

 

**WebMvcConfigurerAdapter**

- org.springframework.web.servlet.config.annotation. WebMvcConfigurerAdapter
- @EnableWebMvc 를 이용하면 대부분의 기본 설정이 모두 자동으로 되지만, 기본 설정 이외의 설정이 필요할 경우 WebMvcConfigurerAdapter를 클래스를 상속 받은 후, 원하는 메소드를 오버라이딩 하여 구현한다.



앞에까지 내용들이 모두 설정과 관련된 내용들이었다면 이제는 사용자가 핸들러 클래스인 컨트롤러를 작성해야 한다.

**Controller(Handler) 클래스 작성하기**

- @Controller 애노테이션을 클래스 위에 붙인다. 그러면 ComponentScan이 컨트롤러로 인식해서 Spring 컨테이너가 관리할 수 있도록 해준다.
- 클래스 위나 메서드 위에다가 맵핑을 위한 @RequestMapping 애노테이션을 사용한다. 요청이 들어왔을 때 어떤 URL로 들어온 요청인지를 알아내서 실제로 처리해야 되는 컨트롤러가 뭔지, 그 컨트롤러에서 구현하고 있는 메서드가 뭔지를 알아내야 한다. 그런데 그냥 알아낼 수는 없기 때문에 RequestMapping 어노테이션을 이용해서 알려줘야한다. 

**@RequestMapping**

- Http 요청과 이를 다루기 위한 Controller 의 메소드를 연결하는 어노테이션
- Http Method 와 연결하는 방법
   - @RequestMapping(value="/users", method=RequestMethod.POST)
   - From Spring 4.3 version (@GetMapping, @PostMapping, @PutMapping, @DeleteMapping, @PatchMapping)
- Http 특정 해더와 연결하는 방법
   - @RequestMapping(method = RequestMethod.GET, headers = "content-type=application/json")
- Http Parameter 와 연결하는 방법
   - @RequestMapping(method = RequestMethod.GET, params = "type=raw")
- Content-Type Header 와 연결하는 방법
   - @RequestMapping(method = RequestMethod.GET, consumes = "application/json")
- Accept Header 와 연결하는 방법
   - @RequestMapping(method = RequestMethod.GET, produces = "application/json")

------

**실습 코드**

WebMvcContextConfiguration.java

```java
package kr.or.connect.mvcexam.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.DefaultServletHandlerConfigurer;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;
import org.springframework.web.servlet.view.InternalResourceViewResolver;

@Configuration
@EnableWebMvc
@ComponentScan(basePackages = { "kr.or.connect.mvcexam.controller" })
public class WebMvcContextConfiguration extends WebMvcConfigurerAdapter {
    //web.xml 파일에서 DispathcerServlet을 설정할 때 모든 요청('/')이 들어올 때 servlet-class 속성 이름에 맞는 특정 서블릿을 실행하도록 했었다. 그런데 이 때 들어오는 모든 요청 중에는 컨트롤러의 URL이 매핑되어있는 요청만 들어오는 게 아니라 CSS,이미지,JS 등등의 것들도 있기 때문에 들어오기 때문에 /assets/, /css/, /img/, /js/등으로 시작하는 URL요청은 어플리케이션 루트 디렉토리 아래에 있는 각각의 디렉토리를 만들어놓고 알맞게 사용하게 나눠서 처리해주어야한다.
	@Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/assets/**").addResourceLocations("classpath:/META-INF/resources/webjars/").setCachePeriod(31556926);
        registry.addResourceHandler("/css/**").addResourceLocations("/css/").setCachePeriod(31556926);
        registry.addResourceHandler("/img/**").addResourceLocations("/img/").setCachePeriod(31556926);
        registry.addResourceHandler("/js/**").addResourceLocations("/js/").setCachePeriod(31556926);
    }
 	
    //파라미터로 전달받은 DefaultServletHandlerConfigurer 객체의 enable이라는 메서드를 호출함으로써 DefaultServletHandler를 사용하도록 해주는 부분이다. 매핑 정보가 없는 URL 요청은 Spring의 DefaultServletHttpRequestHandler가 처리하도록 해준다. Spring의 DefaultServletHttpRequestHandler는 WAS의 DefaultServlet에게 해당 일을 넘기게 된다. 그러면 WAS는 DefaultServlet이 static한 자원을 읽어서 보여주게 해주는 것이다. 
    // default servlet handler를 사용하게 합니다.
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }
   //addViewControllers  메서드는 특정 URL에 대한 처리를 컨트롤러 클래스를 작성하지 않고 매핑할 수 있도록 해주는 것이다. 여기에서 보면 "/"라는 요청 자체가 들어오면 main이라고 하는 이름의 view로 보여주도록 하는 것이다. 이 main은 어디서 찾아낼 수 있을까? view name은 viewResolver라는 객체를 이용해서 찾는다고 했었다. 실제 "main"이라는 이름만 가지고는 뷰 정보를 찾아낼 수 없다. 뷰 정보는 getInternalResourceViewResolver 메서드에서 설정된 형태로 뷰를 사용하게 된다.
    @Override
    public void addViewControllers(final ViewControllerRegistry registry) {
    		System.out.println("addViewControllers가 호출됩니다. ");
        registry.addViewController("/").setViewName("main");
    }
    
    //설정되어 있는 것을 보면 InternalResourceViewResolver를 생성을 하고 있고 이 InternalResourceViewResolver에게 setPrefix, setSuffix를 지정하고 있는 것을 볼 수 있다. 즉, main 앞쪽에 접두어로 setPrefix의 설정 값을 붙여주고, main 뒤 쪽에 접미어로 setSuffix의 설정 값을 붙여준다. 결국 "/"의 요청이 들어왔을 때 이동하게 되는 뷰의 경로는 WEB-INF/views/main.jsp가 된다.
    @Bean
    public InternalResourceViewResolver getInternalResourceViewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        return resolver;
    }
}
```



DispatcherServlet이 실제로 동작을 하게 하기 위해서 DispatcherServlet을 FrontServlet으로 등록해야 한다. Java config spring 설정을 읽어들이도록 web.xml에 설정을 해야지만 Spring이 제공하는 Dispatcher Servlet이 실제 FrontController의 역할을 할 수 있을 것이다.

web.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns="https://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="https://xmlns.jcp.org/xml/ns/javaee https://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" version="3.1">

  <display-name>Spring JavaConfig Sample</display-name>

  <servlet>
  	//아래 servlet-mapping을 통해 요청이 들어오면 아래 서블릿을 찾게 된다.
    <servlet-name>mvc</servlet-name>
    //Spring이 제공하고 있는 DispatcherServlet을 FrontController로 설정하는 부분
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      //context 클래스가 등록되고 있다. IoC 실습하면서 Bean공장이 필요했다. 현재 서블릿이 실행이 될 떄는 AnnotationConfigWebApplicationContext를 사용하겠다는 설정이다.
      <param-name>contextClass</param-name>
      <param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext</param-value>
    </init-param>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      //위에서 작성했던 java configuration 설정 파일 클래스로 등록하여 읽도록 하는 부분
      <param-value>kr.or.connect.mvcexam.config.WebMvcContextConfiguration</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
  	//모든 요청이 들어오면 servlet-name에 등록되어 있는 서블릿 클래스가 실행된다.
  	//servlet-name이 mvc였으므로 servlet-name이 똑같은 위의 코드에 servlet element 안에 있는 servlet-name이 mvc인 이름을 찾아 갈 것이다.
    <servlet-name>mvc</servlet-name>
    //모든 요청
    <url-pattern>/</url-pattern>
  </servlet-mapping>


</web-app>
```

main.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<h1>main page~~~!!</h1>
</body>
</html>
```



위의 실습에서 

org.springframework.web.servlet.PageNotFound noHandlerFound 경고: No mapping found for HTTP request with URI [/mvcexam/] in DispatcherServlet with name 'mvc'

에러 때문에 정말 거의 3주를 날렸다. 물론 실제로 쏟은 시간은 3~4일 정도겠지만.. 진도를 거의 못나갔다. 그래서 기록해두고자 edwith에 남긴 댓글 기록을 남긴다.

---

아래 제가 남겼던 질문을 해결해서 혹시 같은 문제에 직면하신 분이 계실까하여 가지고 왔습니다. 원인으로는 여러 가지 이유가 있었을 것 같습니다만.. 아마도 jsp 파일을 로딩하지 못했거나, config 클래스를 인지하지 못한 것 같았습니다. 계속 noHandlerFound이라고 나오더라고요. 오타는 아니었습니다. 프로젝트를 똑같이 몇 번을 따라했습니다. 복사도 하고, 직접 쳐 보기도하고, web.xml / WebMvcContextConfigution.java / pom.xml 수십번 읽은 것 같네요. 너무 오랫동안 고생해서 혹시나 같은 문제에 직면하신 분들은 시간 낭비하지 마시라고 댓글 남깁니다 ㅠㅠ
에러 메시지:
org.springframework.web.servlet.PageNotFound noHandlerFound
경고: No mapping found for HTTP request with URI [/mvcexam/] in DispatcherServlet with name 'mvc'

강의 예시 코드와 다른 부분입니다.

1. pom.xml에 다음의 코드를 추가합니다.

~~~xml
<!-- https://mvnrepository.com/artifact/org.apache.tomcat.embed/tomcat-embed-jasper -->
<dependency>
<groupId>org.apache.tomcat.embed</groupId>
<artifactId>tomcat-embed-jasper</artifactId>
<version>자신의 톰캣버전을 적으세요(예를들면, 8.5.13)</version>
</dependency>
~~~

2. WebMvcContextConfiguration.java 에서

~~~java
@Bean
public InternalResourceViewResolver getInternalResourceViewResolver() {
    System.out.println("InternalResourceViewResolver가 호출됩니다.");
    InternalResourceViewResolver resolver = new InternalResourceViewResolver();
    resolver.setViewClass(JstlView.class);
    resolver.setPrefix("/WEB-INF/views/");
    resolver.setSuffix(".jsp");
    return resolver;
  }
~~~

resolver.setViewClass(JstlView.**class**); 이 부분을 추가해 줬습니다
그리고 가장 중요한 server 초기화입니다.
위의 코드들을 추가하시고, 

1. servers 탭에서 servers를 완전히 delete합니다. 
2. Project Explorers에서도 Servers를 완전히 delete합니다.
3. 그리고 Maven update를 합니다.
4. 이클립스 상단의 Project tap에서 clean을 진행합니다.
5. 프로젝트를 우클릭하여 Run on server를 진행합니다.
   그러면 아마 강의 내용처럼 정상적으로 /WEB-INF/views/main.jsp가 보이는 것을 확인하실 수 있을 거에요.

(그리고 프로젝트명 우클릭 - properties - maven - Java EE Integration 체크. 이 부분도 강의 영상에는 없습니다만, 저는 예전 영상 다시 보면서 체크했습니다. 만약 안 되어있다면 이 부분도 해보세요.) 

---

**Controller작성 실습 1/3**

1. 웹 브라우저에서 <https://localhost:8080/mvcexam/plusform> 이라고 요청을 보 내면 서버는 웹 브라우저에게 2개의 값을 입력받을 수 있는 입력 창과 버튼이 있는 화면을 출력한다.
2. 웹 브라우저에 2개의 값을 입력하고 버튼을 클릭하면 <https://localhost:8080/mvcexam/plus> URL로 2개의 입력값이 POST방식으로 서버에게 전달한다. 서버는 2개의 값을 더한 후, 그 결과 값을 JSP에게 request scope으로 전달하여 출력한다.

**Spring MVC가 지원하는 Controller메소드 인수 타입**

따라서 HttpServletRequest를 사용하고 싶다던가, HttpServletResponse를 사용하고 싶다던가, Session을 쓰고 싶다던가 할 때 controller의 메서드에 해당 부분을 선언해주기만 하면 된다. 그러면 spring이 자동으로 넣어주므로 가져다 쓸 수 있다. 굵게 표시된 것들이 현재 수업에서 사용해야하는 것들이다.

- javax.servlet.ServletRequest
- **javax.servlet.http.HttpServletRequest**
- org.springframework.web.multipart.MultipartRequest
- org.springframework.web.multipart.MultipartHttpServletRequest
- javax.servlet.ServletResponse
- **javax.servlet.http.HttpServletResponse**
- **javax.servlet.http.HttpSession**
- org.springframework.web.context.request.WebRequest
- org.springframework.web.context.request.NativeWebRequest
- java.util.Locale
- java.io.InputStream
- java.io.Reader
- java.io.OutputStream
- java.io.Writer
- javax.security.Principal
- java.util.Map
- org.springframework.ui.Model
- org.springframework.ui.ModelMap
- **org.springframework.web.multipart.MultipartFile** (part 6에서 사용)
- javax.servlet.http.Part
- org.springframework.web.servlet.mvc.support.RedirectAttributes
- org.springframework.validation.Errors
- org.springframework.validation.BindingResult
- org.springframework.web.bind.support.SessionStatus
- org.springframework.web.util.UriComponentsBuilder
- org.springframework.http.HttpEntity<?>
- Command 또는 Form 객체

**Spring MVC가 지원하는 메소드 인수 애노테이션**

RequestParam에 이것을 가져오고 싶어요. RequestHeader에 이것을 가져오고 싶어요.

- **@RequestParam**
- **@RequestHeader**
- **@RequestBody**
- @RequestPart
- **@ModelAttribute**
- **@PathVariable**
- @CookieValue

**@RequestParam**

- Mapping된 메소드의 Argument에 붙일 수 있는 어노테이션
- @RequestParam의 name에는 http parameter의 name과 멥핑
  - HTML form 태그에 input 상자에 지정된 name과 mapping되어서 여기에 지정된 name에 있는 값을 꺼내는 것이다.
- @RequestParam의 required 속성은 필수인지 아닌지를 판단

**@PathVariable**

실제 URL path에서 path에다가 '?변수명 = 값'과 같은 형식으로 값을 넘겨주는데, 이 값을 받기 위해 사용되는 어노테이션이다.

- @RequestMapping의 path에 변수명을 입력받기 위해서는 place holder가 필요함
- place holder의 이름과 PathVariable의 name 값과 같으면 mapping 됨
- required 속성은 default가 true 임

이런 부분들을 이용할 때 항상 주의할 점은 사용자가 넣어준 이름을 근거로 Spring이 대신 알아서 매핑해주는 것이므로, 넣어준 이름과 메서드 파라미터에 넣은 변수명하고 일치해야지 정상적으로 매핑을 해줄 것이다. 이 부분을 잘 확인하기.

**@RequestHeader**

- 요청 정보의 헤더 정보를 읽어들 일 때 사용
- @RequestHeader(name="헤더명") String 변수명

**Spring MVC가 지원하는 메소드 리턴 값**

Controller 메서드가 리턴할 때 리턴할 수 있는 리턴 값의 종류들이다.

- **org.springframework.web.servlet.ModelAndView**
- org.springframework.ui.Model
- java.util.Map
- org.springframework.ui.ModelMap
- org.springframework.web.servlet.View
- **java.lang.String**
- java.lang.Void
- org.springframework.http.HttpEntity<?>
- org.springframework.http.ResponseEntity<?>
- **기타 리턴 타입**

------

**실습 코드**

plusForm.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<form method="post" action="plus">  
value1 : <input type="text" name="value1"><br>
value2 : <input type="text" name="value2"><br>
<input type="submit" value="확인">  
</form>  
</body>
</html>
```

plusResult.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
${value1} 더하기 ${value2} (은/는) ${result} 입니다.
</body>
</html>
```

PlusController.java

```java
package kr.or.connect.mvcexam.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class PlusController {
    //plusform이라는 url요청이 들어오면 plusform이라는 문자열을 반환해서, InternalResourceViewResolver가 /WEB-INF/views/plusfor.jsp로 url을 변경하여 접근한다.
	@GetMapping(path = "/plusform")
	public String plusform() {
		return "plusForm";
	}

    //plusform에서 값을 두 개 넘겨서 보내면, 이 값 두개를 받아서 더 한 다음에 이 값을 request scope에 넣어서 넘겨주면 해당 jsp가 값들을 출력한다.
	@PostMapping(path = "/plus")
    //메서드의 인자에 굉장히 많은 것들이 넘어간다. 여기에도 어노테이션이 쓰이고 있다.
    //plusform.jsp에서 input안의 값이 name이 value1으로 설정되어 넘어오는데, @RequestParam에 value1으로 들어오는 이 값을 controller가 가진 plus라는 메서드 내에서는 int 타입의 변수 value1으로 사용하겠다는 뜻.
	public String plus(@RequestParam(name = "value1", required = true) int value1,
			@RequestParam(name = "value2", required = true) int value2, ModelMap modelMap) {
        
        //HttpServletRequest를 import해서 직접 request scope에 setAttribute를 사용하여 request에 값을 지정해도 되지만, 그렇게 되면 HttpServletRequest에 종속되어 버리므로 직접 쓰지 않고 spring이 제공하고 있는 modelmap이라는 객체를 받아서 이 객체에 넣어준다. 이렇게 넣어주면 spring이 알아서 reqeust scope에 매칭시켜준다. 그러면 이걸 가져다가 사용하면 된다. spring을 사용할 때에 HttpServletRequest를 받아서 직접 사용할 수도 있지만 spring이 제공하는 다양한 객체들이 존재하므로 알맞은 객체를 가져다가 사용하는 것이 좋다.
        
		int result = value1 + value2;

		modelMap.addAttribute("value1", value1);
		modelMap.addAttribute("value2", value2);
		modelMap.addAttribute("result", result);
		return "plusResult";
	}
}
```



servers에 mvcexam이 이미 등록되어 있으므로  web.xml을 바꿨을 때에는 아얘 servers에서 mvcexam 우클릭하여 삭제하고 다시 실행을 시키면 된다. 이래도 안되면 project-clean을 해볼 것. clean은 eclipse가 내부적으로 잘 못 가지고 있거나 엉켜있는 설정들을 다시 정리해준다.

1. web.xml을 바꿨을 때
   1. servers탭을 열고 하위에 등록된 현재 프로젝트 삭제
   2. 이클립스 상단 project 탭에서 clean 실행
   3. run on server
2. pom.xml을 바꿨을 때 혹은 java 파일 이름이나 jsp파일 이름 등의 directory 구조를 바꿨을 때 
   1. maven update
3. JSP, java 파일을 새로 생성하거나, 내용을 변경했을 때
   1. 서버 재시작



 **Controller작성 실습 2/3**

1. https://localhost:8080/mvcexam/userform 으로 요청을 보내면 이름, email, 나이를 물어보는 폼이 보여진다.
2. 폼에서 값을 입력하고 확인을 누르면 post방식으로 https://localhost:8080/mvcexam/regist 에 정보를 전달하게 된다.
3. regist에서는 입력받은 결과를 콘솔 화면에 출력한다.

**Controller작성 실습 3/3**

1. https://localhost:8080/mvcexam/goods/{id} 으로 요청을 보낸다.
   1. 이렇게 중괄호로 넘기는 것을 path variable이라고 한다. 이렇게 받았을 때 어떻게 받는지를 연습해본다.
2. 서버는 id를 콘솔에 출력하고, 사용자의 브라우저 정보를 콘솔에 출력한다.
3. 서버는 HttpServletRequest를 이용해서 사용자가 요청한 PATH정보를 콘솔에 출력한다.

------

**실습 코드**

userform.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<form method="post" action="regist">  
name : <input type="text" name="name"><br>
email : <input type="text" name="email"><br>
age : <input type="text" name="age"><br>
<input type="submit" value="확인"> 
</body>
</html>
```

UserController.java

```java
package kr.or.connect.mvcexam.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import kr.or.connect.mvcexam.dto.User;

@Controller
public class UserController {
    //지난 예제에서는 GetMapping으로 수행을 했었다.
    //아래와 같은 코드도 똑같은 기능을 한다.
	@RequestMapping(path="/userform", method=RequestMethod.GET)
	public String userform() {
		return "userform";
	}
	
    //plusform에서는 @RequestParam을 통해서 값을 하나하나 받았다. 하지만 값을 여러개 전달할 때는 여러 개를 넣을 수 있는 가방 역할인 DTO을 만들어서 전달했었다. 따라서 DTO User를 만들고 여기에 넣어서 전달한다.
    //@ModelAttribute 어노테이션을 붙여주고 객체를 선언하면 spring mvc가 userForm.jsp 에서 name 속성을 가지고 넘어온 값들을 꺼내서 UserController의 User객체를 생성하고 이 객체 안에 넘어온 값들을 담아준다.
	@RequestMapping(path="/regist", method=RequestMethod.POST)
	public String regist(@ModelAttribute User user) {

		System.out.println("사용자가 입력한 user 정보입니다. 해당 정보를 이용하는 코드가 와야합니다.");
		System.out.println(user);
		return "regist";
	}
}
```

 

User.java

```java
package kr.or.connect.mvcexam.dto;

public class User {
	//접근자는 private으로 3개의 칼럼 추가
    private String name;
	private String email;
	private int age;
    
    //외부에서 private접근자인 name, email, age에 접근할 수 있도록 getter, setter 추가
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
    
    //어떤 데이터들이 들어있는지 확인할 수 있게 toString 추가
	@Override
	public String toString() {
		return "User [name=" + name + ", email=" + email + ", age=" + age + "]";
	}	
}
```

regist.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
<h2>등록되었습니다.</h2>
</body>
</html>
```

goodsById.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
id : ${id } <br>
user_agent : ${userAgent }<br>
path : ${path }<br>
</body>
</html>
```

GoodsController.java

```java
package kr.or.connect.mvcexam.controller;

import javax.servlet.http.HttpServletRequest;

import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestHeader;

@Controller
public class GoodsController {

	@GetMapping("/goods/{id}")
    //url 요청이 들어왔을 때 뒤에 들어오는 값을 path variable로 받는다는 뜻. id라는 이름으로 넘어온 것을 int변수 id로 쓰겠다는 뜻. 
    //Request Header를 통해 헤더에서 넘어오는 변수들을 받아서 String 변수로 사용한다.
    //Request가 가진 값들을 꺼내서 보여주기 위해 HttpServletRequest를 사용한다. 종속되기 때문에 가급적이면 사용하지 않는 것이 좋다고 했지만 꼭 사용할 수 밖에 없는 경우가 있을 수 있다. 
    //ModelMap을 통해 값을 전달을 시켜주먄 JSP가 해당 값들을 꺼내서 사용할 수 있게 된다.
	public String getGoodsById(@PathVariable(name="id") int id,
							   @RequestHeader(value="User-Agent", defaultValue="myBrowser") String userAgent,
							  HttpServletRequest request,
							  ModelMap model
							  ) {
		
		String path = request.getServletPath();
		
		System.out.println("id : " + id);
		System.out.println("user_agent : " + userAgent);
		System.out.println("path : " + path);
		
		model.addAttribute("id", id);
		model.addAttribute("userAgent", userAgent);
		model.addAttribute("path", path);
		return "goodsById";
	}
}
```

------

**생각해보기**

1. SpringMVC를 이용해서 웹 어플리케이션을 개발하는 것과 서블릿을 이용해 개발하는 것과 비교해보면 어떤 장단점이 있다고 생각하세요?



**참고 자료**

[![img](https://cphinf.pstatic.net/mooc/20180219_1/1519005924957WqtFg_PNG/vqqCHR7IDcLcwZlBXyTy.png?type=mfullfill_199_148)](https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java)

- **[참고링크] WebMvcConfigurationSupport**<https://github.com/spring-projects/spring-framework/blob/master/spring-webmvc/src/main/java/org/springframework/web/servlet/config/annotation/WebMvcConfigurationSupport.java>

  spring-framework - Spring Framework

- **[참고링크] Web on Servlet Stack**<https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html>



