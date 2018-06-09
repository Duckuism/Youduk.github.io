---
layout: post
title: Redirect, Forward
excerpt: "Redirect와 Forward의 개념, 차이, Jsp와 Servlet의 연동"
tags: [Boostcourse]
categories: [JSP, Servlet]
link:
comments: true
pinned: true
image:
  feature:
---

## Redirect

#### 리다이렉트 (redirect) : 서버가 클라이언트에게 특정 URL로 이동하라는 요청을 보내는 것

- 리다이렉트는 HTTP프로토콜로 정해진 규칙이다.
- 서버는 클라이언트로부터 요청을 받은 후, 클라이언트의 요청에 대해 특정 URL로 이동을 요청할 수 있다. 이를 리다이렉트라고 한다.
- 서버는 클라이언트에게 HTTP 상태코드 302로 응답하는데 이때 헤더 내 Location 값 안에 이동할 URL 을 추가한다. 클라이언트는 302 코드 리다이렉션 응답을 받게 되면 헤더 안의 Location에 포함된 URL로 재요청을 보내게 된다. 이때 브라우저의 주소창은 새 URL로 바뀌게 된다.
- 서블릿이나 JSP는 리다이렉트하기 위해 HttpServletResponse 클래스의 sendRedirect() 메소드를 사용한다.



 **실습코드**

- redirect01.jsp, redirect02.jsp 파일을 작성
- 웹 브라우저가 redirect01.jsp을 요청
- redirect01은 redirect02.jsp로 리다이렉팅하는 로직이 실행되도록 함
- 결과 확인

WebContent/redirect01.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
    response.sendRedirect("redirect02.jsp");
%>    
```

다른건 아무것도 안 한다. 응답이 필요없이 특정 URL로 redirect 하라는 코드만 작성할 것이다. JSP가 아니더라도 Servlet에서도 똑같은 코드를 작성한다면 redirect를 할 수 있다. redirect는 response라는 객체가 가지고 있는 sendRedirect() 메서드를 실행하면된다. 인자 값으로 redirect할 URL을 넣어준다.



WebContent/redirect02.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
	redirect된 페이지입니다.
</body>
</html>
```

redirect가 되었다는 것을 확인할 수 있는 text를 입력한다.



그리고 redirect01.jsp를 run on server하면, redirect02 페이지로 redirect된 것을 볼 수 있다.



![](/img/Redirect_1.png)

위의 그림에서 redirect01요청 응답 코드가 302인 것을 확인할 수 있다.

![](/img/Redirect_2.png)

위에서부터 순서대로 실행된다.

1. 브라우저에서 WAS로 redirect01.jsp 요청
2. WAS가 브라우저에게 redirect02로 redirect 요청 (응답코드:302, Location헤더 값:redirect02.jsp)
3. 웹 브라우저는 WAS의 redirect 요청을 받고 redirect02.jsp를 요청
4. redirect02.jsp 결과 출력
5. 브라우저 주소창 URL이 redirect02.jsp로 바뀜

위의 과정에서 클라이언트가 요청을 1번, 3번에서 두 번 보냈다는 것을 기억해야한다. 항상 요청이 들어갈때 request 객체와 response 객체가 생성되는데, 1번에서의 request/response 객체와 3번에서의 request/response 객체는 다르다는 것을 알아야 한다.



[**[참고링크] Servlet Tutorial: sendRedirect method - javatpoint**](https://www.javatpoint.com/sendRedirect()-method)

[**[참고링크] HTTP 상태 코드**](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

[**[참고링크] HTTP Status Code**](http://ooz.co.kr/260)

[**[참고링크] Redirections in HTTP**](https://developer.mozilla.org/ko/docs/Web/HTTP/Redirections)

[**[참고링크] URL Shortener and Link Management Platform**](https://bitly.com/)

[**[참고링크] Google URL Shortener**](https://goo.gl/)



## Forward

#### Forward : WAS의 서블릿이나 JSP가 요청을 받은 후 그 요청을 처리하다가, 추가적인 처리를 같은 웹 어플리케이션안에 포함된 다른 서블릿이나 JSP에게 위임하는 행위

![](/img/Forward_1.png)

1. 웹 브라우저에서 WAS에게 요청을 보내고, Servlet1에서 요청을 받음
2. Servlet1은 요청을 일정 부분만 처리한 후, 그 결과를 HttpServletRequest에 저장
3. Servlet1은 결과가 저장된 HttpServletRequest와 응답을 위한 HttpServletResponse를 같은 웹 어플리케이션 안에 있는 Servlet2에게 전송 **(이렇게 넘겨주는, 위임하는 작업을 forward라고 한다.)**
4. Servlet2는 Servlet1으로 부터 받은 HttpServletRequest와 HttpServletResponse를 이용하여 요청의 남은 부분을 처리한 후 웹 브라우저에게 결과를 전송

Forward를 통해 결과를 보내는 Servlet1과 결과를 받는 Servlet2는 서로의 변수를 쓸 수 없다. Servlet1, Servlet2 모두 지역변수를 선언하여 작업을 처리하기 때문이다. 그렇기 때문에 forward를 통해 Servlet1의 결과를 받아서 Servlet2가 처리하기 위해서는 Servlet1과 Servlet2 모두가 사용할 수 있는 객체가 필요하다. 이 조건에 부합하는 것이 request/response객체이다. request객체와 response객체는 요청 처리가 끝날 때까지 없어지지 않는다. 따라서 Servlet1의 결과를 Servlet2에서 또 사용해야한다면 Servlet1의 결과를 request객체에 저장한 후, Servlet2에서 request객체를 읽어서 다시 요청을 처리하는 방식으로 진행해야 한다.



#### Redirect와 Forward의 차이

- Redirect는 클라이언트가 서버에서 요청을 보내면 서버는 요청을 처리하고 **다시 클라이언트에게** 새로 요청할 곳을 알려주면서 응답을 보내고, 클라이언트는 서버에서 또 다른 요청을 보낸다. 그리고 서버는 또 다른 요청에 맞는 처리를 한 후 응답을 다시 한 번 보낸다. 클라이언트와 서버가 총 2번씩 요청을 주고 받는 것! 따라서 Redirect 결과는 실제 처리 다음에 URL주소가 바뀌는 것이다. (2번째 요청의 결과)
- Forward는 클라이언트는 요청을 한 번 보내면 서버쪽에서 여러 리소스가 나눠서 요청을 처리한 후 응답을 보내는 것이다. 따라서 URL이 바뀌지 않는다. (요청, 응답이 1번 뿐이므로)



#### Forward 실습

- 2개의 서블릿을 작성 : FrontServlet, NextServlet
- http://localhost:8080/firstweb/front
  - 위의 URL이 호출되면 FrontServlet이 실행됨
  - FrontServlet에서는 랜덤한 주사위 값을 구하고, 그 값을 NextServlet에게  forward
  - NextServlet에서는 FrontServlet으로부터 전달받은 주사위 값만큼 "hello"를 출력

JavaResouces/src/examples/FrontServlet.java

```java
package examples;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


@WebServlet("/front")
public class FrontServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    public FrontServlet() {
        super();
    }

	protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	    int diceValue = (int)(Math.random()*6+1); // 주사위 눈이 6개라고 생각했을 때 이 값을 NextServlet에 넘겨서 출력을 할 것이다. 여기서 해야할 일 첫 번째는 diceValue를 request 객체에 저장해서 NextServlet에서 쓸 수 있게 하는 것이다.
        request.setAttribute("dice", diceValue); //dice라는 key값과 diceValue라는 value값을 매칭하여 request에 저장한다. 이 때 diceValue는 기존의 int 형이 아닌 object형으로 저장된다. (어떤 타입이든 상관없이 저장해야 하므로)
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/next"); //redirect에서는 request.sendRedirect()라는 메서드를 이용했듯이, request할 때는 request가 가지고 있는 requestDispatch() 메서드가 존재한다. requestDispatcher 객체를 request로부터 getRequestDispatcher() 메서드를 통해 얻어낸다. 이 때 인자값은 어디로 이동할 것인지를 명시한다. 즉 이 RequestDispatcher 객체는 request를 받아서 올바른 목적지 URL로 이동시키는 역할이다. 인자 값을 넣을 때 주의할 점은 forward할 경로는 상대경로고, 같은 웹 어플리케이션 안에서만 가능하다는 것이다.
        requestDispatcher.forward(request, response);//requestDispatcher객체가 가지고 있는 forward()메서드를 수행하면 된다. 이 때 반드시 넘겨줘야할 값은 처음 요청 시 받아왔던 request, response 객체이다.
	}

}
```

FrontServlet의 요청 주소로 지정한 /front로 요청이 들어왔을 때 WAS는 요청을 추상화한 객체 HttpServletRequest와 응답을 추상화한 객체 HttpServletResponse를 만든다. 그리고 FrontServlet의 service() 메서드가 호출 될 때 각각의 인자 값에 이 객체 두 개를 넣어서 보내준다. 

JavaResouces/src/examples/NextServlet.java

```java
package examples;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/next")
public class NextServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public NextServlet() {
        super();
    }

    protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html");
        PrintWriter out = response.getWriter();
        out.println("<html>");
        out.println("<head><title>form</title></head>");
        out.println("<body>");

        int dice = (Integer)request.getAttribute("dice"); //저장했던 key값으로 request에서 값을 찾아온다. setAttribute로 값을 저장할 때, 타입에 상관없이 저장을 하기 위해 Object로 저장하므로 찾아올 때는 Integer로 형 변환이 필요하다.
        out.println("dice : " + dice);
        for(int i = 0; i < dice; i++) {
            out.print("<br>hello");
        }
        out.println("</body>");
        out.println("</html>");
    }

}
```



이렇게 코드를 작성하고 FrontServlet을 run on server 하면 아래와 같은 창을 얻을 수 있다. Hello 출력 횟수가 run 할 때마다 random하게 바뀐다.

![](/img/Forward_2.png)

redirect와는 달리 URL이 바뀌지 않은 것을 알 수 있다.



#### **생각해보기**

1. 서블릿은 프로그램 로직을 개발하기에 편리하지만, HTML 태그를 출력하기엔 불편합니다. JSP는 프로그램 로직을 개발하기는 좀 불편하지만, HTML 태그를 출력하기엔 편리합니다. 서블릿과 JSP는 서로 장단점이 반대입니다. 포워드를 이용해서 이러한 단점을 해결하고 싶습니다. 어떻게 해야 할까요?
   - JSP를 통해 페이지를 구현하고 필요한 값을 request 객체에 담아 서블릿으로 포워드하여 프로그램 로직을 개발할 수 있습니다.



- [**[참고링크] Servlet forward example - How to forward from a servlet to a JSP**](https://alvinalexander.com/blog/post/servlets/forwarding-from-servlet-jsp)



## Servlet & Jsp연동

서블릿과 JSP는 상호 보완적인 관계를 가지고 있다. 

서블릿은 로직을 구현하기에 알맞지만, HTML을 출력하기엔 불편하다. 반대로 JSP는 로직을 구현하는 것은 불편하지만 HTML을 출력하기엔 편리하다. 이러한 서블릿과 JSP를 좀 더 잘 사용하기 위해서 forward가 사용되는 경우가 많다. 

#### **Servlet과 JSP연동**

- Servlet은 프로그램 로직이 수행되기에 유리하다. Java 파일이므로 IDE 등에서 지원을 좀 더 잘해준다.
- JSP는 결과를 출력하기에 Servlet보다 유리하다. 필요한 html문을 그냥 입력하면 됨.
- 프로그램 로직 수행은 Servlet에서, 결과 출력은 JSP에서 하는 것이 유리하다.
- Servlet과 JSP의 장단점을 해결하기 위해서 Servlet에서 프로그램 로직이 수행되고, 그 결과를 JSP에게 포워딩하는 방법이 사용되게 되었다. 이를 Servlet과 JSP연동이라고 한다.

![](/img/Servlet&Jsp_1.png)



#### 실습

- LogicServlet에서 1부터 100사이의 random한 값 2개와, 그 값의 합을 구한 후 그 결과를 result.jsp에게 포워딩하는 방법으로 전송하여 결과를 출력한다.

Java Resources/src/examples/LogicServlet.java

```java
package examples;

import java.io.IOException;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet("/LogicServlet")
public class LogicServlet extends HttpServlet {
    private static final long serialVersionUID = 1L;

    public LogicServlet() {
        super();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        int v1 = (int)(Math.random() * 100) + 1;
        int v2 = (int)(Math.random() * 100) + 1;
        int result = v1 + v2;
        
        request.setAttribute("v1", v1);
        request.setAttribute("v2", v2);
        request.setAttribute("result", result);
        
        RequestDispatcher requestDispatcher = 	request.getRequestDispatcher("/result.jsp");
        requestDispatcher.forward(request, response);
    }

}

```



WebContent/result.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
EL표기법으로 출력합니다.<br>
${v1} + ${v2} = ${result} <br><br>

스클립틀릿과 표현식을 이용해 출력합니다.<br>
<%
    int v1 = (int)request.getAttribute("v1");
    int v2 = (int)request.getAttribute("v2");
    int result = (int)request.getAttribute("result");
%>

<%=v1%> + <%=v2 %> = <%=result %>
</body>
</html>
```



이렇게 코드를 작성한 후 LogicServlet을 run on server하면 랜덤한 두 값을 더한 값이 출력되는 것을 확인 할 수 있다. 즉 랜덤으로 값을 뽑는 것과 뽑힌 값 두개를 더하는 것은 LogicServlet.java에서 수행하고, 결과 값을 변수에 저장한 후 request객체에 담아서 forward하면, result.jsp에서는 request에 담겨있는 LogicServlet의 결과값을 읽어서 출력한다.

Jsp가 출력을 담당하지만 디자인 적인 부분이 아닌 자바 코드가 계속 보여지는 것은 그다지 바람직하지 않다. 따라서 이 부분을 대체할 수 없을까? 하는 생각을 하게 되고, 그래서 나오게 된 것이 EL, JSTL이다.

- EL태그 ```${key값}``` : 이렇게 기입을 하면 request를 뒤져서 알아서 key값에 맞는 value를 꺼내온다.

JSP에서는 되도록 자바코드를 줄이는 것이 좋다.



**생각해보기**

1. 객체지향에서 객체는 관련된 것들을 모아서 가지고 있는 특징이 있습니다. 웹 페이지 URL도 관련된 URL이 있습니다. 예를 들어, 게시판 글쓰기, 읽기, 목록 보기 등은 모두 게시판과 관련된 URL일 것입니다. 하지만 지금까지의 예제들을 보면 서블릿은 하나의 URL만 처리하고 있습니다. 하나의 서블릿이 여러 개의 요청을 받을 수는 없을까요?
   (힌트 : 서블릿 URL mapping에서 와일드카드('*'기호)를 사용하는 방법에 대해서 조사해보세요.)

 

[**[참고링크] URL Patterns**](http://docs.roguewave.com/hydraexpress/3.5.0/html/rwsfservletug/4-3.html)

