---
layout: post
title: Spring Core
excerpt: "Spring이란?, Spring loC/DI 컨테이너, xml파일을 이용한 설정, Java Config를 이용한 설정"
tags: [Boostcourse]
categories: [Spring]
link:
comments: true
pinned: true
image:
  feature: spring.png
---

# 1) Spring이란?

Framework : 반제품. 완전한 제품은 아니지만 어느정도 틀이 갖춰져 있어서 내가 원하는 대로 약간의 커스텀을 할 수 있는 느낌. 전체적으로 보면 형상이나 모양은 같지만, 세세한 부분은 만드는 사용자에 따라 달라질 수 있다. 즉 복잡하고 어려운 부분은 이미 구현되어 있는 것이다.



**들어가기 전에**

이번 시간엔 Spring Framework가 무엇인지, 그리고 Spring Framework를 구성하고 있는 모듈에는 어떠한 것들이 있는지 알아보도록 하겠습니다.

------

**학습 목표**

1. Spring Framework가 무엇인지 이해합니다.
2. Spring Framework에는 어떤 모듈들이 있는지 이해합니다.

------

**핵심 개념**

- Spring Framework
- Spring Framework modules

 

**Spring Framework란?**

- 엔터프라이즈급 어플리케이션(기업형. 큰 어플리케이션)을 구축할 수 있는 가벼운 솔루션이자, 원스-스탑-숍(One-Stop-Shop) 
  - 원-스탑
- 원하는 부분만 가져다 사용할 수 있도록 모듈화가 잘 되어 있습니다.
- IoC 컨테이너입니다.
- 선언적으로 트랜잭션을 관리할 수 있습니다.
- 완전한 기능을 갖춘 MVC Framework를 제공합니다.
- AOP 지원합니다.
- 스프링은 도메인 논리 코드와 쉽게 분리될 수 있는 구조로 되어 있습니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_180/1517452205302mNfIy_PNG/2_10_1___.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20655/#)

- **프레임 워크 모듈**

   

**프레임 워크 모듈**

- 스프링 프레임워크는 약 20개의 모듈로 구성되어 있습니다.
- 필요한 모듈만 가져다 사용할 수 있습니다.

**AOP 와 인스트루멘테이션 (Instrumentation)**

- spring-AOP : AOP 얼라이언스(Alliance)와 호환되는 방법으로 AOP를 지원합니다.
- spring-aspects : AspectJ와의 통합을 제공합니다.
- spring-instrument : 인스트루멘테이션을 지원하는 클래스와 특정 WAS에서 사용하는 클래스로 더 구현체를 제공합니다. 참고로 BCI(Byte Code Instrumentations)은 런타임이나 로드(Load) 때 클래스의 바이트 코드에 변경을 가하는 방법을 말합니다.

**메시징(Messaging)**

- spring-messaging : 스프링 프레임워크 4는 메시지 기반 어플리케이션을 작성할 수 있는 Message, MessageChannel, MessageHandler 등을 제공합니다. 또한, 해당 모듈에는 메소드에 메시지를 맵핑하기 위한 어노테이션도 포함되어 있으며, Spring MVC 어노테이션과 유사합니다.

 

**데이터 엑서스(Data Access) / 통합(Integration)**

- 데이터 엑세스/통합 계층은 JDBC, ORM, OXM, JMS 및 트랜잭션 모듈로 구성되어 있다.
- **spring-jdbc** : 자바 JDBC프로그래밍을 쉽게 할 수 있도록 기능을 제공합니다.
- **spring-tx** : 선언적 트랜잭션 관리를 할 수 있는 기능을 제공합니다.
- spring-orm : JPA, JDO및 Hibernate를 포함한 ORM API를 위한 통합 레이어를 제공합니다.
- spring-oxm : JAXB, Castor, XMLBeans, JiBX 및 XStream과 같은 Object/XML 맵핑을 지원합니다.
- spring-jms : 메시지 생성(producing) 및 사용(consuming)을 위한 기능을 제공, Spring Framework 4.1부터 spring-messaging모듈과의 통합을 제공합니다.

**웹(Web)**

- 웹 계층은 spring-web, spring-webmvc, spring-websocket, spring-webmvc-portlet 모듈로 구성됩니다.
- **spring-web** : 멀티 파트 파일 업로드, 서블릿 리스너 등 웹 지향 통합 기능을 제공한다. HTTP클라이언트와 Spring의 원격 지원을 위한 웹 관련 부분을 제공합니다.
- **spring-webmvc** : Web-Servlet 모듈이라고도 불리며, Spring MVC 및 REST 웹 서비스 구현을 포함합니다.
- spring-websocket : 웹 소켓을 지원합니다.
- spring-webmvc-portlet : 포틀릿 환경에서 사용할 MVC 구현을 제공합니다.

------

**생각해보기**

1. 스프링은 프레임워크라고 합니다. 프레임워크와 라이브러리는 어떤 차이가 있을까요? 조사해보세요.

------

**참고 자료**

- **[참고링크] Spring Framework Reference Documentation**<https://docs.spring.io/spring/docs/4.3.14.RELEASE/spring-framework-reference/htmlsingle/#overview>


- **[참고링크] Java BCI(Byte Code Instrumentation) 간단 예제와 설명**<https://deidesheim.tistory.com/entry/%EC%9E%90%EB%B0%94-BCIByte-Code-Instrumentation-%EA%B0%84%EB%8B%A8-%EC%98%88%EC%A0%9C%EC%99%80-%EC%84%A4%EB%AA%85>


# 2) Spring IoC/DI 컨테이너

**들어가기 전에**

이번 시간엔 스프링 프레임워크의 핵심 개념 중의 하나인 IoC와 DI에 대해 학습하도록 하겠습니다.

------

**학습 목표**

1. 컨테이너에 대한 개념을 이해한다.
2. IoC에 대한 개념을 이해한다.
3. DI에 대한 개념을 이해한다.

------

**핵심 개념**

- Container

  - 인스턴스의 생명주기를 관리한다.
  - 생성된 인스턴스들에게 추가적인 기능을 제공한다.
  - 인스턴스를 생성해서 실행하고 인스턴스가 소멸되는 작업들을  사용자가 직접 하지 않고 대신 해주는 것이 Container.
  - 서블릿을 배울 때 서블릿을 정의하긴 했지만, 서블릿 클래스를 인스턴스화하는 과정을 직접하지는 않았다. 이 일을 tomcat이 대신 해줬는데, 이렇게 서블릿을 실행시켜주는 WAS는 서블릿 컨테이너를 갖고 있다는 뜻이다. WAS는 웹 브라우저로부터 서블릿 url에 해당하는 요청을 받으면 서블릿을 메모리에 올린 후에 실행을 하게 된다. 개발자가 서블릿 클래스를 작성했지만 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet 컨테이너가 해주는 것. Servlet 컨테이너는 동일한 Servlet에 해당하는 요청을 받으면 또 메모리에 올리지 않고 기존에 메모리에 올라간 Servlet을 실행해서 그 결과를 웹브라우저에게 전달하는 역할을 해준다. 
  - JSP도 마찬가지였다. JSP파일을 생성하긴 했지만 이 JSP가 서블릿으로 바뀌고, 서블릿이 인스턴스를 만들고 하는 과정도 tomcat이라는 WAS가 대신 실행해줬다.
  - 위의 서블릿, JSP처럼 인스턴스의 생명주기를 관리하는 것을 컨테이너라고 하는 것.

- IoC (Inversion of Control)

  - IoC란 Inversion of Control의 약어이다. Inversion은 사전적 의미로는 '도치, 역전'이다. 보통 Ioc를 제어의 역전이라고 번역한다.

  - 개발자는 프로그램의 흐름을 제어하는 코드를 작성한다. 그런데, 이 흐름의 제어를 개발자가 하는 것이 아니라 다른 프로그램이 그 흐름을 제어하는 것을 IoC라고 말한다.

  - 만약 TV와 리모컨이 있다고 해보자. SamsungTV을 사용하다가 LG TV로 바꿨는데 각각 딸려온 리모컨이 가지고 있는 동일한 모양의 버튼이 기능이 다르다면? SamsungTV를 사용하던 사용자 입장에서는 바뀐 LG TV 리모컨을 사용하기가 굉장히 어려울 것이다. 그래서 이러한 상황을 방지하기 위해 리모컨은 어느 정도의 동일한 버튼 모양, 위치, 기능 등이 일정하게 만들어진다. 이렇게 일정하게 정해진 규격 껍데기를 **인터페이스**라고 부른다. 프로그래밍에서도 인터페이스를 이용한다. 
    <br>

    만약 SamsungTV를 보는 기능을 구현한다고 생각하면, 먼저 tv를 ```S_TV stv = New S_TV()``` 와 같은 형식으로 생성했을 것이다. 그런데 이 과정에서 생성자의 내용이 각자 다르다면 멤버 변수와 메서드가 모두 다를 것이므로 TV마다 사용하는 방법이 천차만별일 것이다. 이 때 위에서처럼 인터페이스를 통해서 공통 멤버 변수, 메서드등을 만들어놓는다면, 주요한 기능들은 TV의 종류에 관계없이 같은 메서드로 실행될 것이다. 보통은 TV라는 인터페이스를 만들고, 이 인터페이스에 TV가 꼭 가져야 하는 기본적인 기능을 넣어놓는다. 그리고 S_TV, L_TV등이 이 인터페이스를 구현하면서 추가적으로 필요한 기능들을 구현해서 생성한다. 실제로 코드를 본다면 ```TV tv = new S_TV()```,  ```TV tv = new L_TV()``` 와 같이 생성할 것이다. 그리고 각각의 tv는 공통 기능이 필요할 때 tv.메서드()의 형식으로 공통 메서드를 사용할 것이다. 
    <br>

    그런데 이렇게 인터페이스를 이용한다고 하더라도, 공통 메서드를 사용 할 때마다 해당 클래스에 맞는 생성자 코드가 실행되어야 한다.

    ~~~java
    //TV 인스턴스를 구현한 S_tv 클래스에서 공통 메서드 show()를 실행할 때
    Tv tv = new S_tv();//S_tv 클래스 생성자 코드 실행
    tv.show();
    
    //TV 인스턴스를 구현한 L_tv 클래스에서 공통 메서드 show()를 실행할 때
    TV tv = new L_tv();//L_tv 클래스 생성자 코드 실행
    tv.show();
    ~~~

    그런데 프로그램 코드가 바뀐다는 것은 컴파일을 모두 다시해야 되는 일이므로 작은 일이아니다. 따라서 이런 부분까지도 변경하지 않고 사용할 수 있는 방법을 강구하게 되었다. 그래서 사용하게 된 것이 '공장'이다. TV Factory같은 것을 하나 만들어놓고 권한을 위임한 다음, 사용자 코드는 변경하지 않게 하는 것이다.

    ~~~java
    TvFactory tvFactory = new TvFactory();
    //이 아래의 사용자 코드는 변하지 않는다.
    TV tv = TVFactory.getTv("S");//실제 사용할 때는 여기에 값을 직접 넣지 않는다. 서블릿의 약속된 어노테이션으로 값을 넣어주거나 web.xml 파일 안에 url패턴과 같은 값이 들어오면 WAS의 Servelt Container가 여기에 해당하는 실제 Servlet 클래스를 만들어서 우리에게 생성해준다.
    tv.show();
    ~~~

    하지만 이렇게 바꾸더라도 TV를 만드려면 TV 공장을 만들어야하고, 다른 걸 만드려면 다른 공장을 매번 만들어야한다. 이 귀찮은 일을 Spring이 대신 해주는 것이다. Spring이 갖고 있는 Bean Factory라던가 Application Context가 이런 역할을 해준다.

- DI (Dependency Injection)

  - DI는 Dependency Injection의 약자로, 의존성 주입이란 뜻을 가지고 있다.
  - DI는 클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말한다.
  - 공장이 인스턴스를 만들었다면 실제로 우리가 써야 한다. 쓰기 위해서는 만들어진 인스턴스 객체를 받아와야 하고, 이 객체를 어떻게 사용할 수 있는지가 고려해야 될 문제이다. DI는 이렇게 만들어진 인스턴스 객체를 사용하기 위해 주입받는 방법 중에 하나라고 생각을 하면 된다. 공장이 만든 인스턴스를 사용하려면 내가 사용하는 프로그램에서 공장이 만든 인스턴스를 가져올 수 있어야 한다. 이 방법에는 여러가지가 있는데 그 중 DI를 공부하는 것이다. DI라고 하는 것은 이렇게 의존적으로 만들어진 인스턴스(의존성)를 내가 사용하는 프로그램으로 가져오는(주입받는) 것을 말한다. 
    

 **컨테이너(Container)**

Servlet을 실행해주는 WAS는 Servlet 컨테이너를 가지고 있다고 말합니다.

WAS는 웹 브라우저로부터 서블릿 URL에 해당하는 요청을 받으면, 서블릿을 메모리에 올린 후 실행합니다.

개발자가 서블릿 클래스를 작성했지만, 실제로 메모리에 올리고 실행하는 것은 WAS가 가지고 있는 Servlet컨테이너입니다.

Servlet컨테이너는 동일한 서블릿에 해당하는 요청을 받으면, 또 메모리에 올리지 않고 기존에 메모리에 올라간 서블릿을 실행하여 그 결과를 웹 브라우저에게 전달합니다.

컨테이너는 보통 인스턴스의 생명주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하는 것을 말합니다.

**IoC** 

예를 들어 서블릿 클래스는 개발자가 만들지만, 그 서블릿의 메소드를 알맞게 호출하는 것은 WAS입니다.

이렇게 개발자가 만든 어떤 클래스나 메소드를 다른 프로그램이 대신 실행해주는 것을 제어의 역전이라고 합니다.

**DI**

DI는 Dependency Injection의 약자로, 의존성 주입이란 뜻을 가지고 있습니다.

DI는 클래스 사이의 의존 관계를 빈(Bean) 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것을 말합니다.

**DI가 적용 안 된 예**

개발자가 직접 인스턴스를 생성합니다.

```java
class 엔진 {

}

class 자동차 {
     엔진 v5 = new 엔진();
}
```

**Spring에서 DI가 적용된 예**

엔진 type의 v5변수에 아직 인스턴스가 할당되지 않았습니다.

컨테이너가 v5변수에 인스턴스를 할당해주게 됩니다.

```java
@Component
class 엔진 {

}

@Component
class 자동차 {
     @Autowired
     엔진 v5;
}
```

DI를 적용함으로써 엔진이라는 인스턴스를 만드는 주체가 바뀌었다. 제어가 역전 된 것이다. 개발자가 사용하는 코드에는 어디에도 new 엔진 인스턴스를 생성하는 코드가 보이지 않을 것이다. Spring에서 해줄 것이기 때문에! 약속된 어노테이션들을 이용해서 선언만 해주면 Spring 컨테이너가 알아서 맞는 객체를 판별하고 인스턴스를 생성해서 주입해줄 것이다.



**Spring에서 제공하는 IoC/DI 컨테이너**

- BeanFactory : IoC/DI에 대한 기본 기능을 가지고 있습니다.
- ApplicationContext : BeanFactory의 모든 기능을 포함하며, 일반적으로 BeanFactory보다 추천됩니다. 트랜잭션처리, AOP등에 대한 처리를 할 수 있습니다. BeanPostProcessor, BeanFactoryPostProcessor등을 자동으로 등록하고, 국제화 처리, 어플리케이션 이벤트 등을 처리할 수 습니다.

- BeanPostProcessor : 컨테이너의 기본로직을 오버라이딩하여 인스턴스화와 의존성 처리 로직 등을 개발자가 원하는 대로 구현 할 수 있도록 합니다.
- BeanFactoryPostProcessor : 설정된 메타 데이터를 커스터마이징 할 수 있습니다.

------

**생각해보기**

1. 스프링 프레임워크는 DI Container라고도 말을 합니다. 스프링 프레임워크 이외에도 DI Container는 존재할까요?

------

**참고 자료**

- **[참고링크] Spring - IoC & DI**<https://isstory83.tistory.com/91>


[![img](https://cphinf.pstatic.net/mooc/20180201_158/1517460788486yvBJi_PNG/lVj4LX3tpD7vajNBs8b0.png?type=mfullfill_199_148)](https://www.nextree.co.kr/p11247/)

- **[참고링크] 세 가지 DI 컨테이너로 향하는 저녁 산책**<https://www.nextree.co.kr/p11247/>



# 3) xml파일을 이용한 설정

**들어가기 전에**

이번 시간엔 Spring의 IoC / DI 컨테이너에 대한 동작을 확인하기 위해 Maven을 이용해 프로젝트를 생성한 후, XML 형식의 설정 파일을 만들어 IoC와 DI가 잘 동작하는지 확인해 보도록 하겠습니다.

------

**학습 목표**

1. Maven을 이용해 스프링 프레임워크를 사용하는 프로젝트를 생성할 수 있습니다.
2. Bean이 무엇인지 이해합니다.
3. XML형식의 스프링 설정파일의 내용을 이해합니다.

------

**핵심 개념**

- Bean
- ApplicationContext
- DI

---

 **Maven으로 Java프로젝트 만들기**

[![img](https://cphinf.pstatic.net/mooc/20180201_190/1517462891679CGmpw_PNG/2_10_3_01.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


[![img](https://cphinf.pstatic.net/mooc/20180201_185/1517463283214IBgVg_PNG/2_10_3_02.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


[![img](https://cphinf.pstatic.net/mooc/20180201_220/1517463299850hKUDB_PNG/2_10_3_03.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- Archetype은 Maven 프로젝트에서 제공해주는 템플릿이다. 어떤 것을 지정하느냐에 따라서 프로젝트 구조가 달라진다. 예제 등이 들어있을 수도 있다. 기업 같은 경우는 자신들만의 Archetype을 만들어서 사용 할 수도 있다.


[![img](https://cphinf.pstatic.net/mooc/20180201_164/1517463316445fpgB3_PNG/2_10_3_04.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- Group Id : 보통 GroupId는 회사의 도메인을 거꾸로 쓴다. 패키지 만드는 규칙과 비슷하다. 나중에 Group Id와 Artifact Id가 패키지가 된다. 따라서 이런 규칙들을 지켜주고 소문자로 사용하는 것이 좋다.

- Artifact Id : 실제 프로젝트 이름을 적어주면 된다.


pom.xml 파일에 JDK를 사용하기 위한 플러그인 설정을 추가합니다.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>kr.or.connect</groupId>
  <artifactId>diexam01</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>diexam01</name>
  <url>https://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  
-------------------------------------추가----------------------------------------------------
  <build>
     <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
  </build>
----------------------------------------------------------------------------------------------

</project>
```

[![img](https://cphinf.pstatic.net/mooc/20180201_32/1517463718873yJ0Mw_PNG/2_10_3_05.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


[![img](https://cphinf.pstatic.net/mooc/20180201_64/15174637391134wWon_PNG/2_10_3_06.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 프로젝트를 선택하고, Maven -> Update Project를 선택합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_267/1517463762791LUfi6_PNG/2_10_3_07.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 위와 같은 창이 뜨면 OK버튼을 클릭합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_186/1517463781375Jws7S_PNG/2_10_3_08.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


[![img](https://cphinf.pstatic.net/mooc/20180201_75/1517463794508OMJeP_PNG/2_10_3_09.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


------

**실습코드**

App.java

```java
package kr.or.connect.diexam01;

/**
 * Hello world!
 *
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "Hello World!" );
    }
}
```

AppTest.java

```java
package kr.or.connect.diexam01;

import junit.framework.Test;
import junit.framework.TestCase;
import junit.framework.TestSuite;

/**
 * Unit test for simple App.
 */
public class AppTest 
    extends TestCase
{
    /**
     * Create the test case
     *
     * @param testName name of the test case
     */
    public AppTest( String testName )
    {
        super( testName );
    }

    /**
     * @return the suite of tests being tested
     */
    public static Test suite()
    {
        return new TestSuite( AppTest.class );
    }

    /**
     * Rigourous Test :-)
     */
    public void testApp()
    {
        assertTrue( true );
    }
}
```

[![img](https://cphinf.pstatic.net/mooc/20180201_217/1517463908421y8xdJ_PNG/2_10_3_10.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- AppTest.java 를 선택한 후 우측버튼을 클릭하고 Run As -> JUnit Test 메뉴를 선택합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_175/1517463930304it65z_PNG/2_10_3_11.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 하단의 JUnit 뷰에 하나의 테스트가 성공했다는 메시지와 함께 녹색 막대가 보여집니다.



위의 부분까지가 간단하게 Maven으로 프로젝트를 하나 만들어보는 과정이다.

이제 DI 테스트를 하기 위해 필요한 것이 무엇일지 생각해본다. DI는 내가 원하는 객체를 내가 생성하는 게 아니라 프레임워크(Spring)이 제공하는 공장이 만들어서 나에게 주입시켜주는 것이다. 이 과정을 테스트해보는 것이므로 공장이 자동으로 만들어줄 객체가 하나 필요한데, 이런 객체를 bean이라고 한다. 예전에는 비주얼한 컴포넌트를 bean이라고 불렀는데, 근래에 들어서는 일반적인 자바 클래스를 bean 클래스라고 부른다.

**Bean class란?**

예전에는 Visual 한 컴포넌트를 Bean이라고 불렀지만, 근래 들어서는 일반적인 Java클래스를 Bean클래스라고 보통 말합니다.

Bean클래스의 3가지 특징은 다음과 같습니다.

- 기본생성자를 가지고 있습니다.
- 필드는 private하게 선언합니다.
- getter, setter 메소드를 가집니다.
- getName() setName() 메소드를 name 프로퍼티(property)라고 합니다. (용어 중요)

그렇다면 왜 Bean 클래스는 이러한 특징을 가지고 있는 것일까? 현재 우리가 사용할 UserBean 클래스는 사용자가 직접 생성하는 것이 아니라 Spring이 해준다. 이 때는 반드시 규칙이 필요하다.

------

**실습코드**

UserBean.java

```java
package kr.or.connect.diexam01;

//빈클래스
public class UserBean {
	
	//필드는 private한다.
	private String name;
	private int age;
	private boolean male;
	
	//기본생성자를 반드시 가지고 있어야 한다.
	public UserBean() {
	}
	
	public UserBean(String name, int age, boolean male) {
		this.name = name;
		this.age = age;
		this.male = male;
	}

	// setter, getter메소드는 프로퍼티라고 한다.
	public void setName(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public boolean isMale() {
		return male;
	}

	public void setMale(boolean male) {
		this.male = male;
	}

}
```

**Spring Bean Factory를 이용하여 Bean객체 이용하기**

1) pom.xml 파일을 다음과 같이 수정합니다.

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>kr.or.connect</groupId>
  <artifactId>diexam01</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>jar</packaging>

  <name>diexam01</name>
  <url>https://maven.apache.org</url>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <spring.version> 4.3.14.RELEASE</spring.version>
  </properties>

  <dependencies>
	<!-- Spring -->
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-context</artifactId>
		<version>${spring.version}</version>
	</dependency>
  
  
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>
  
  <build>
     <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.6.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
  </build>
</project>
```

properties에 추가하는 것들은 상수처럼 사용할 수 있는 것들이다. dependency나 pom.xml 안에서 특정 값(버전명 등)의 참조가 지속적으로 필요한 경우가 있다. 그럴 때 값 자체로 사용하는 것이아니라 properties 안의 태그 이름으로 참조해서 사용하는 것이다. 위의 코드에서 spring dependency에서는 properties에서 선언한 spring.version태그 이름을 ${}안에 넣어서 사용함으로서 4.3.14.RELEASE라는 스프링 버전 값을 가져왔다.

2) 추가된 라이브러리 확인합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_238/1517464099184UKyw9_PNG/2_10_3_12.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 


3) resources 소스 폴더를 생성합니다.

resources 폴더 안의 파일들은 Spring에게 정보를 준다. 소스랑 자바 파일이랑 섞여있으면 복잡하므로 따로 관리해주려고 만드는 것.

[![img](https://cphinf.pstatic.net/mooc/20180201_270/1517464138494xeh5V_PNG/2_10_3_13.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 프로젝트를 선택하고, 오른쪽 버튼을 클릭한 후 New -> Folder를 선택합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_240/1517464159150ItjGr_PNG/2_10_3_14.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- src/main 폴더를 선택한 후 forder name에 resources라고 Finish버튼을 클릭합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_68/15174641827232pkY5_PNG/2_10_3_15.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 해당 폴더를 선택하고, 우측버튼을 클릭하여 New – File을 선택합니다. src/main/resources 폴더를 선택한 후 File name에 applicationContext.xml 을 입력하고 Finish버튼을 클릭합니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_93/1517464203430V601P_PNG/2_10_3_16.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 위와 같이 생성되었으면 더블클릭하여 파일을 엽니다.

4) resources 소스 폴더에 xml 파일을 작성합니다.

------

**실습코드** 

applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="https://www.springframework.org/schema/beans"
	xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="https://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="userBean" class="kr.or.connect.diexam01.UserBean"></bean>

</beans>
```

xml파일로 spring 설정 파일을 만들 때 가장 바깥쪽 태그를 root element라고 한다. 이 root element가 반드시 beans여야 한다. 그리고 xml 스키마에 대한 설정도 되어있어야 한다. spring container가 이 파일을 읽어들이는데 beans 태그 안에 아무것도 없으면 아무 작업도 하지 않을 것이다.

지금 우리가 하고 싶은 것은 Spring container한테 내가 사용할 객체를 대신 생성하게 하고 싶은 것이다. 따라서 반드시 Spring container한테 사용할 정보를 제공해야한다. 이 때 사용되는 element가 자바의 일반적인 class를 나타내는 bean element이다. bean element에다가 몇 가지 속성을 지정해서 추가하면 spring container가 해당 정보를 읽어서 객체를 생성하고 주입해준다.

bean 태그를 하나 입력했는데, 위의 태그는 다음과 같은 의미를 가집니다.

UserBean userBean - new UserBean();

kr.or.connect.diexam01.UserBean userBean = new kr.or.connect.diexam01.UserBean();

Spring container는 이런 객체를 하나만 생성해서 가지고 있다. 이렇게 객체를 딱 하나만 가지고 있는 것을 싱글턴 패턴이라고 한다.

이제 Spring 설정 파일을 작성했으니까 이 설정 파일을 읽어들이는 객체도 하나 생성해야한다.



**ApplicationContext를 이용해서 설정파일을 읽어들여 실행하기**

ApplicationContextExam01

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ApplicationContextExam01 {

	public static void main(String[] args) {
		ApplicationContext ac = new ClassPathXmlApplicationContext( 
				"classpath:applicationContext.xml"); 
		System.out.println("초기화 완료.");
		
		UserBean userBean = (UserBean)ac.getBean("userBean");
		userBean.setName("kim");
		System.out.println(userBean.getName());
		
		UserBean userBean2 = (UserBean)ac.getBean("userBean");
		if(userBean == userBean2) {
			System.out.println("같은 인스턴스이다.");
		}
		
	}
}
```

- 이 클래스를 만드는 이유는 프로그램을 시작시킬 시작점이 필요하기 때문이다.
  1. main 메서드를 만든다.
  2. Spring이 가진 공장을 생성해야하므로 Spring이 가지고 있는 공장인 ApplicationContext를 만드는 코드를 작성한다.
  3. 인터페이스인 ApplicationContext를 구현하는 여러 클래스들이 있는데 위의 코드에서는 이 중 ClassPathXmlApplicationContext라는 객체를 생성해서 사용한다.
  4. 이 ClassPathXmlApplicationContext객체에 인자값으로 자동 생성할 객체 정보를 담아놨던 applicationContext.xml의 정보를 입력하고, 공장에게 bean정보를 넣어놓았으니 이 정보를 가지고 공장을 세우라고 지정한다.
  5. 잘 동작하는지 콘솔 출력을 통해 확인한다.
  6. 공장에서 생성해서 얻어올 객체가 UserBean이므로 이름을 그대로 선언하고 getBean()메서드를 이용해서 ac라는 이름의 applicationContext 공장에서 생성된 bean을 얻어온다. 이 때 getBean()은 무조건 Object 타입으로 생성된 객체를 반환하므로 형변환이 필요하다.
  7. applicationContext 공장은 userBean이라는 정보를 가지고 applicationContext.xml에서 일치하는 id가 있는지 찾고, 찾으면 같이 등록되어있는 클래스 정보를 가지고 클래스를 생성한다. 그리고 생성한 클래스를 반환한다.
  8. bean을 하나 얻어왔다면 이 얻어온 bean에 메서드를 실행해서 제대로 작동하는지 확인한다.
  9. 그리고 객체를 하나 더 받아와서 기존에 받아왔던 인스턴스랑 비교해본다. 연산자를 사용하여 비교하면 두 개의 인스턴스가 같다고 나오는데, 이 결과를 통해 ApplicationContext가 하나의 객체만 사용하는 싱글턴 패턴을 이용하고 있다는 사실을 확인할 수 있다. 사용자가 계속 getBean()을 이용해 요청을 하더라도 이 객체를 그 때마다 계속 만들어내는 것이 아니라 하나 만든 bean을 이용하는 것이다.

- 영상 우측 하단에 자막 스크립트 ON 설정을 한 후 강의를 시청하시면 학습에 도움이 됩니다.

resouces 폴더는 main폴더 안에 들어있다. 이 resources 폴더는 소스 폴더이다. 따라서 resources폴더에서 생성한 xml 파일은 자동으로 classpath로 지정이 된다. 같은 계층에 있는 java 폴더에서 만들어진 클래스들과 마찬가지로 bean 폴더에 생성된다. 이 때문에 ClassPathXmlApplicationContext에서 사용할 수 있는 것이다.

ClassPathXmlApplicationContext 인스턴스가 생성될 때는 생성자 파라미터로 지정된 설정 파일을 읽어들인 후에 이 파일안에 선언된 bean들을 모두 메모리에 올려놓는다. 이 때 문제가 발생하면 해당 어플리케이션은 종료가 된다. 이렇게 메모리에 올려놨으므로 getBean() 메서드에 인스턴스를 얻고자는 클래스의 xml 설정에 적힌 id 값을 넘겨주면, 해당 인스턴스를 반환한다. 이 때 인스턴스의 타입은 여러가지가 될 수 있으므로 getBean() 메서드는 항상 Object 타입으로 결과를 반환한다.

이렇게 객체를 대신 생성해주고 싱글턴으로 관리해주는 기능 등을 'IoC(제어의 역전)'이라고 한다.



**DI 확인하기**

이번에는 DI 즉 의존성 주입을 확인해보도록 하겠습니다.

Car와 Engine이라는 클래스 2개를 생성합니다.

------

**실습코드**

Engine.java

```java
package kr.or.connect.diexam01;

public class Engine {
	public Engine() {
		System.out.println("Engine 생성자");
	}
	
	public void exec() {
		System.out.println("엔진이 동작합니다.");
	}
}
```

Car.java

```java
package kr.or.connect.diexam01;

public class Car {
	Engine v8;
	
	public Car() {
		System.out.println("Car 생성자");
	}
	
	public void setEngine(Engine e) {
		this.v8 = e;
	}
	
	public void run() {
		System.out.println("엔진을 이용하여 달립니다.");
		v8.exec();
	}
}
```

위의 Car 클래스가 제대로 동작하도록 하려면 보통 다음과 같은 코드가 작성되야 합니다.

```java
Engine e = new Engine();
Car c = new Car();
c.setEngine( e );
c.run();
```

1, 2 번째 줄을 Spring 컨테이너에게 맡기기 위해 설정파일에 다음과 같은 코드를 입력합니다.

여기서 property는 getter, setter 메서드를 말한다. bean 태그에 파일을 등록하면 해당 클래스를 자동으로 생성하지만, setEngine() 과 같은 getter, setter 메서드는 대신 실행해주지 않는다. 이런 메서드를 해결하려면 property 태그를 통해 강제적으로 연결해주어야 한다. property 태그의 ref 속성은 id가 e로 지정되어 있는 클래스를 생성해서 참조한 후 사용하겠다는 얘기이다. 여기서는 setEngine() 메서드에 id가 e로 선언된 인스턴스를 파라미터로 전달해준다는 의미를 가지는 것이다.

```xml
<bean id="e" class="kr.or.connect.diexam01.Engine"></bean>
<bean id="c" class="kr.or.connect.diexam01.Car">
	<property name="engine" ref="e"></property>
</bean>
```

즉, 위의 XML설정은 다음과 같은 의미를 가집니다.

```java
Engine e = new Engine();
Car c = new Car();
c.setEngine( e );
```

이번엔 위의 설정 파일을 읽어들여 실행하는 ApplicationContextExam02.java를 작성해보도록 하겠습니다.

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public class ApplicationContextExam02 {

	public static void main(String[] args) {
        //ClassPathXmlApplicationContext는 applicationContext.xml에 설정해놓은 정보를 가지고 bean을 생성한다. 따라서 해당 xml 파일에 대한 정보를 넘겨준다.
		ApplicationContext ac = new ClassPathXmlApplicationContext( 
				"classpath:applicationContext.xml"); 
		//자동차 객체를 생성하는 주체가 내가 아니라 Spring container인 ApplicationContext가 된다. 따라서 ApplicationContext가 갖고 있는 getBean() 메서드를 이용하고, applicationContext.xml에 등록했던 Bean id를 넘겨주면 된다. 이 코드가 실행되면 엔진을 탑재한 자동차 객체가 만들어진다.
		Car car = (Car)ac.getBean("c");
        //자동차 객체가 가진 run() 메서드 실행
		car.run();
		
	}
}
```

콘솔을 보면 다음과 같이 실행된 것을 알 수 있습니다.

[![img](https://cphinf.pstatic.net/mooc/20180201_145/1517469480126MWiKv_PNG/2_10_3_17.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/20657/#)

- 위와 같이 어떤 객체에게 객체를 주입하는 것을 DI라고 한다. DI를 사용할 때의 자점은 무엇일까? 코드에서는 Car라는 클래스만 등장하고 Engine이라는 클래스는 실행 클래스에서 등장하지 않는다. 이 말은 사용자는 사용할 Car라는 클래스만 알고 있으면 된다는 말과 같다. 

- 만약 전기 엔진 버스를 만든다고해보자. 그렇다면 Car를 상속받고 있는 Bus라는 클래스가 생성되도록 xml파일만 바꿔주고 Bus가 상속받고 있는 Engine 클래스도 Electric Engine으로 주입받도록 바꿔준다면 실행클래스의 코드는 하나도 바뀌지 않고 전기 엔진 버스가 만들어질 수 있다.

- 스프링이 버전업이 되면서 xml보다는 어노테이션과 자바 Config를 함께 사용해서 설정하는 방법이 더 많이 이용되고 있다. 일일히 bean을 등록하는 과정 자체도 불편하다고 생각한 것.


**생각해보기**

- Spring컨테이너가 관리하는 객체를 빈(Bean)이라고 말합니다. (여러분들이 직접 new연산자로 생성해서 사용하는 객체는 빈(Bean)이라고 말하지 않습니다.) Spring은 빈을 생성할 때 기본적으로 싱글톤(Singleton)객체로 생성합니다. 싱글톤이란 메모리에 하나만 생성한다는 것입니다. 메모리에 하나만 생성되었을 경우, 해당 객체를 동시에 이용한다면 어떤 문제가 발생할 수 있을까요? 이런 문제를 해결하려면 어떻게 해야할까요?   ( 참고로 Spring에서 빈을 생성할 때 스코프(scope)를 줄 수 있습니다. 스코프를 줌으로써 기본으로 설정된 싱글톤 외에도 다른 방법으로 객체를 생성할 수 있습니다. )

------

**참고 자료**

- **[참고링크] Appendix C. XML Schema-based configuration**<https://docs.spring.io/spring/docs/3.0.x/spring-framework-reference/html/xsd-config.html>


- <https://www.slipp.net/wiki/pages/viewpage.action?pageId=25528177>



# 4) Java Config를 이용한 설정

**들어가기 전에**

이번 시간엔 Java Config와 어노테이션을 이용해 스프링에서 사용하는 빈을 정의하고 DI하는 방법에 대해 알아보도록 하겠습니다.

------

**학습 목표**

1. JavaConfig형태의 설정파일의 내용을 이해할 수 있습니다.
2. @ComponentScan, @Component, @Autowired 어노테이션의 쓰임새에 대해 이해합니다.

------

**핵심 개념**

- AnnotationConfigApplicationContext
- @Configuration
- @ComponentScan
- @Component
- @Autowired



**Java Config를 이용해 설정하기**

ApplicationConfig.java

```java
package kr.or.connect.diexam01;
import org.springframework.context.annotation.*;

@Configuration
public class ApplicationConfig {
	@Bean
    //이 메서드를 호출하게 되면
	public Car car(Engine e) {
        //Car라는 객체를 만들고
		Car c = new Car();
        //Car 객체의 setEngine()이라는 메서드에 주입받은 엔진을 넣어서 생성을 해서
		c.setEngine(e);
        //Car 객체를 리턴한다.
		return c;
	}
	
	@Bean
	public Engine engine() {
		return new Engine();
	}
}
```

@Configuration 은 스프링 설정 클래스라는 의미를 가집니다.

JavaConfig로 설정을 할 클래스 위에는 @Configuration가 붙어 있어야 합니다.

ApplicationContext중에서 AnnotationConfigApplicationContext는 JavaConfig클래스를 읽어들여 IoC와 DI를 적용하게 됩니다.

이때 설정파일 중에 @Bean이 붙어 있는 메소드들을 AnnotationConfigApplicationContext는 자동으로 실행하여 그 결과로 리턴하는 객체들을 기본적으로 싱글턴으로 관리를 하게 됩니다.

이제 설정파일을 읽어서 실행시켜주는 java 파일을 만들어본다.

ApplicationContextExam03.java

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class ApplicationContextExam03 {

	public static void main(String[] args) {
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig.class);
		//ApplicationConfig 파일에서 car 객체를 가져온다.   
		Car car = (Car)ac.getBean("car");
		car.run();
		
	}
}
```

ApplicationContextExam02에서는 ClassPath에서 설정을 읽어왔기 때문에 ClassPathXmlApplicationContext를 사용했지만 ApplicationContextExam03에서는 어노테이션 설정파일을 읽어들일 것이므로 AnnotationConfigApplicationContext를 사용하고, 매개변수로는 설정 정보를 가지고있는 클래스 파일을 넘겨준다.

이렇게 되면 bean을 만들어내는 AnnotationConfigApplicationContext라는 공장이 ApplicationConfig.class가 가지고 있는 설정 정보를 읽어들여서 공장을 세우게 될 것이고, bean들을 만들어서 갖고 있게 된다. 그리고 사용자 요청이 들어오면 알맞은 결과를 줄 것이다.



파라미터로 요청하는 class 타입으로 지정 가능합니다.

Car car = ac.getBean(Car.class);

ApplicationConfig2.java

```java
package kr.or.connect.diexam01;
import org.springframework.context.annotation.*;

@Configuration
@ComponentScan("kr.or.connect.diexam01")
public class ApplicationConfig2 {
}
```

기존 JavaConfig에서 빈을 생성하는 메소드를 모두 제거했습니다.

단, @Configuration아래에 @ComponentScan이라는 어노테이션을 추가했습니다.

@ComponentScan어노테이션은 파라미터로 들어온 패키지 이하에서 @Controller, @Service, @Repository, @Component 어노테이션이 붙어 있는 클래스를 찾아 메모리에 몽땅 올려줍니다.

기존의 Car클래스와 Engine클래스 위에 @Component를 붙이도록 하겠습니다. 이 Componenet는 Class의 소문자를 기본형으로 하고, id처럼 이름을 정해줄 수 있다.

Engine.java

```java
package kr.or.connect.diexam01;

import org.springframework.stereotype.Component;

@Component
public class Engine {
	public Engine() {
		System.out.println("Engine 생성자");
	}
	
	public void exec() {
		System.out.println("엔진이 동작합니다.");
	}
}
```

Car.java

```java
package kr.or.connect.diexam01;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class Car {
	@Autowired
	private Engine v8;
	
	public Car() {
		System.out.println("Car 생성자");
	}
	
	public void run() {
		System.out.println("엔진을 이용하여 달립니다.");
		v8.exec();
	}
}
```

@Autowired는 Engine타입의 객체가 생성된 것이 있으면 알아서 v8에 주입하라는 뜻이다. @Autowired를 사용하면 기존의 setEngine()과 같은 setter 메서드가 필요없게 된다.

수정된 JavaConfig를 읽어들이여 실행하는 클래스를 보도록 하겠습니다.

ApplicationContextExam04.java

```java
package kr.or.connect.diexam01;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class ApplicationContextExam04 {

	public static void main(String[] args) {
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig2.class);
		   
		Car car = ac.getBean(Car.class);
		car.run();
		
	}
}
```

Spring에서 사용하기에 알맞게 @Controller, @Service, @Repository, @Component 어노테이션이 붙어 있는 객체들은 ComponentScan을 이용해서 읽어들여 메모리에 올리고 DI를 주입하도록 하고, 이러한 어노테이션이 붙어 있지 않은 객체는 @Bean어노테이션을 이용하여 직접 생성해주는 방식으로 클래스들을 관리하면 편리합니다.

ComponentScan은 약속된 어노테이션이 붙어있는 것들만 읽어온다. 그런데 나중에 Spring JDBC 혹은 다른 라이브러리가 갖고 있는 객체들을 사용할 때는 라이브러리를 열어서 어노테이션을 붙일 수 없으므로, 이 때는 ApplicationConfig처럼 bean을 등록하는 방법을 이용해서 사용하여야 한다.



------

**생각해보기**

- 다루는 빈(Bean)이 많아질수록 xml로 설정하는 것과 @ComponentScan, @Component, @Autowired를 이용하는 것 중 어떤 것이 유지보수에 좋을 것 같습니까?
- @AutoWired 는 Field, Constructor, Setter Method 에 사용할 수 있습니다. 각각의 방식에 장단점에 대해서 더 생각해보세요.

------

**참고 자료**

- **[참고링크] Spring JavaConfig Reference Guide**<https://docs.spring.io/spring-javaconfig/docs/1.0.0.M4/reference/html/>


- **[참고링크] Field Dependency Injection Considered Harmful**<https://vojtechruzicka.com/field-dependency-injection-considered-harmful/>