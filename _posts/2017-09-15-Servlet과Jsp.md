---
layout: post
title: JSP와 Servlet
excerpt: ""
categories: [Servlet/JSP/Spring]
link:
comments: true
---

전체 프린트 다 감쌀 때 윈도우 알트 쉬프트 에이 컬럼 편집.
쉬프트 커멘드 엘 하면 단축키 목록

톰캣 실행 위치 Downloads/apache-tomcat-8.5.13/bin/startup.sh

###### 참고 영상 : http://olc.oss.kr/lec/detail.jsp?lecid=254
###### 참고 자료 : https://github.com/keesun/servlet2spring/tree/master/src/whiteship
강의 주제 : 서블릿&jsp 프로그래밍에서 spring MVC 프로그래밍으로의 변화 과정

* 서블릿 등장 배경 : 웹페이지가 처음 나왔을 때는 정적인 html 페이지만 보여줄 수 있었다. 그래서 내용이 바뀌는 동적인 페이지들을 보여주고 싶었다.
  1. 첫번째 방법 - CGI(common gateway interface) : 단점이 요청 당 프로세스 방법이라 동시 접속자를 많이 유지 할 수 없었다.
  2. 두번째 방법 - 서블릿 : CGI의 단점을 보완하기 위해 요청 당 쓰레드 방법으로 제공하기 시작했다. 프로세스가 사용하는 자원을 공유하는 많은 쓰레드(프로세스 안의 프로세스)를 만들어서 더 많은 동시 접속자를 유지하게 하는 방법이었다.

servlet2springmvc 라는 클래스 생성
whiteship 이라는 패키지 생성
HelloServlet 이라는 서블릿 생성

command + option + s = generate override 단축키

이름을 받아서 hello랑 같이 출력하는 코드

이 서블릿을 쓰려면 web.xml에 등록을 해줘야 한다.


그러나 실제로 이렇게 화면을 구성하는 경우는 없다. html태그를 넣어줘야 한다.
이렇게 나오기는 하지만 서블릿으로 html 코딩을 하는 것이 굉장히 불편하다.

서블릿의 사용 후기
* 자바 코딩은 편하다.
* 화면(html)을 작성하는 코드를 맞추기 힘들다.
* 매번 web.xml에 서블릿 맵핑 코드를 추가하는 것이 번거롭고 힘들다.
-> 이것에 대한 보완으로 jsp가 등장했다.

JSP의 사용 후기
* 화면(html)코드는 쉽게 작성할 수 있다.
* 자바 코드를 사용하기 힘들다.
-> jsp와 서블릿을 같이 사용해볼까?
-> 화면코드는 jsp로, 자바 코드는 서블릿으로.

~~~java

서블릿 맵핑 퀴즈 : /whiteship/book.do 를 입력했을 때 어느 서블릿에 맵핑될까?

<servlet-mapping>
  <servlet-name>a</servlet-name>
  <url-pattern>*.do</url-pattern>
</servlet-mapping>

<servlet-mapping>
  <servlet-name>b</servlet-name>
  <url-pattern>/whiteship/book</url-pattern>
</servlet-mapping>

<servlet-mapping>
  <servlet-name>c</servlet-name>
  <url-pattern>/whiteship/*</url-pattern>
</servlet-mapping>

정답은 b. (가장 긴 것이므로)

~~~

서블렛 맵핑 규칙
1. 요청 URL과 정확히 일치하는 서블릿 맵핑 사용
2. 디렉토리까지 일치하는 서블릿 맵핑 사용
3. 확장자가 일치하는 서블릿 맵핑 사용
4. 동일한 수준에서 대응하는 맵핑이 여러개라면 그 중에서 가장 긴 것을 사용

hello.jsp 파일을  WEB-INF 안에 views 폴더를 만들어서 그 안으로 집어 넣는다. WEB-INF안에 파일은 브라우저에서 접근이 불가하다. 개발자만 접근할 수 있으므로 보안 측면에서 좋다.

servlet과 jsp를 합친 model2를 사용해보니
* 서블릿으로 자바 코딩하기 편하다.
* jsp로 화면을 작성하기 편하다.
* 이 모습이 MVC와 비슷하다.
Model(지금은 없지만 보통은 javaBeans로 모델을 만들고)
View(JSP가 담당)
Controller(servlet이 담당)

![Smithsonian Image](/img/2017-09-15-01.png)<br />

model2로 만족할 수 있는가?

* 서블릿을 실행하기 전/후에 부가적인 작업을 추가하고 싶다.
* 컨트롤러 하나로 모든 요청을 처리할 수 없을까?
* 요청 처리가 끝나고 보여줄 뷰를 좀 더 편하게 제공할 수는 없을까?
-> J2EE 패턴을 보자!

J2EE 패턴

1. J2EE - decorating pattern : 전/후 처리기가 필요할 때, 기존 코드를 수정하지 않고 부가 기능을 추가할 수 있다.

![Smithsonian Image](/img/2017-09-15-02.PNG)<br />


servlet필터를 사용해보니
* 서블릿 코드를 수정하지 않고 부가기능을 추가할 수 있어 좋다. (기존의 서블릿 코드는 두고 필터를 정의할 때 원하는 기능 추가)
* 하나의 필터(TimerFilter)로 여러 서블릿/URL(예제에서는 url패턴으로 적용)에 부가 기능을 추가할 수 있어 좋다.
* web.xml에 매번 설정하는 것이 번거롭다. (어쨌든 필터 정의, 맵핑을 해줘야 한다.)
* init()과 destroy()도 매번 구현해야하는 것이 번거롭다. (만약 예제와 같은 간단한 예제가 아니라면 이 두가지도 구현해줘야 한다.)

servlet필터 적용 규칙(우선 순위)
컴파일러가 web.xml에서 <file-mapping>을 보고..
1. <url-pattern>에 대응하는 것을 web.xml에 정의된 순서대로 적용
2. <servlet-name>에 대응하는 것을 추가로 적용

servlet필터는 언제 사용할 수 있을까?
* request 필터링 : 보안 관련 내용 체크, 요청 헤더와 바디 포맷팅 수정, 요청 감시 또는 기록
* response 필터링 : 응답스트림압축, 응답스트림에 내용 추가 또는 수정, 전혀 다른 응답으로 교체

2. J2EE - Front Controller 패턴 : 컨트롤러 하나로 모든 요청을 처리하고 싶을 때, 일관된 뷰 관리, 네비게이션, 요청 처리 기능을 한 곳으로 모을 수 있다. 즉, 1번처럼 여러개 의 서블릿을 등록하는 것이 아니라 서블릿은 하나만 등록하고, 자기가 실행하고 싶은 기능들로 요청이 들어왔을 때 맵핑을 해주고 실행한 후, 실행이 끝나면 찾아갈 뷰까지 찾아줄 수 있는 패턴(dispatcher view 패턴 역할까지 같이 할 수 있는 - front controller 패턴 안에 dispatcher기능을 넣으면 dispatcher를 사용할 필요가 없다.)

![Smithsonian Image](/img/2017-09-15-03.PNG)<br />


3. J2EE - Dispatcher View 패턴 : Front Controller 패턴에서 View를 찾아오는 기능을 dispatcher에 위임하는 패턴

![Smithsonian Image](/img/2017-09-15-04.PNG)<br />


*WhiteshipServlet 만들어보기.

![Smithsonian Image](/img/2017-09-15-05.PNG)<br />

WhiteshipServlet의 부족한 점
* 핸들러 맵핑 로직을 변경할 수 없다.
* 핸들러를 여러 형태로 만들 수 없다.
* 예외 처리 로직을 제공하지 않는다.
* 뷰를 찾는 로직을 변경할 수 없다.
-> 스프링 mvc를 사용하는게 났겠다.

Spring = 현존하는 가장 유연한 MVC프레임 워크
* 핸들러 맵핑 로직을 변경할 수 있다.
* 핸들러를 여러 형태로 만들 수 있다.
* 다양한 예외 처리 로직을 제공한다.
* 뷰를 찾는 로직을 변경할 수 있다.

![Smithsonian Image](/img/2017-09-15-06.PNG)<br />
