---
layout: post
title: Layered Architecture 실습
excerpt: ""
tags: [Boostcourse]
categories: [Spring]
link:
comments: true
pinned: true
image:
  feature: spring.png
---

# 2) 레이어드 아키텍처(Layered Architecture) 실습



**들어가기 전에**

이번 시간엔 방명록을 Spring 프레임워크를 이용해 만들어 보도록 하겠습니다.

이를 통해 각 레이어별로 어떤 내용들을 작성해야 하는지 알아보고, 완전히 동작하는 웹 어플리케이션을 개발해 봄으로써 Spring 웹 어플리케이션에 대한 이해를 높이는 시간이 될 수 있길 바랍니다.

------

**학습 목표**

1. Spring 프레임워크를 이용한 웹 어플리케이션 프로젝트를 구성할 수 있습니다.
2. Spring 프레임워크를 이용한 웹 어플리케이션 개발 시 어떤 요소들을 개발해야하는지 이해합니다.

------

**핵심 개념**

- @Controller
- @Service
- @Repository
- @Transactional



방명록 만들기 실습

* Spring JDBC를 이용한 Dao 작성
* Controller + Service + Dao
* 트랜잭션 처리
* Spring MVC에서 폼 값 입력받기
* Spring MVC에서 redirect하기
* Controller에서 jsp에게 전달한 값을 JSTL과 EL을 이용해 출력하기

방명록 요구사항 1/6

* 방명록 정보는 guestbook 테이블에 저장된다.
* id 컬럼은 자동으로 입력된다.
* id, 이름, 내용, 등록일을 저장한다.

방명록 요구사항 2/6

* http://localhost:8080/guestbook/을 요청하면 자동으로 /guestbook/list로 리다이렉팅 한다.
* 방명록이 없으면 건수는 0이 나오고 아래에 방명록을 입력하는 폼이 보여진다.

방명록 요구사항 3/6

* 이름과 내용을 입력하고, 등록 버튼을 누르면 /guestbook/write/URL로 입력한 값을 전달하여 저장한다.
* 값이 저장된 이후에는 /guestbook/list로 리다이렉트 된다.

방명록 요구사항 4/6

* 입력한 한 건의 정보가 보여진다. (캡쳐 화면의 이미지는 입력된 방명록을 삭제한 이후에 입력해서 ID가 15가 되었다.)
* 방명록 내용과 폼 사이의 숫자는 방명록 페이지 링크. 방명록 5건당 1페이지로 설정한다.

방명록 요구사항 5/6

* 방명록이 6건 입력되자 아래 페잊이 수가 2건 보여진다. 1페이지를 누르면 /guestbook/list?start=0을 요청하고, 2페이지를 누르면 /guestbook/list?start=5를 요청하게 된다.
* /guestbook/list는 /guestbook/list?start=0과 결과가 같다.

방명록 요구사항 6/6

* 방명록에 글을 쓰거나, 방명록의 글을 삭제할 때는 Log테이블에 클라이언트의 ip주소, 등록(삭제) 시간, 등록/삭제(method칼럼) 정보를 데이터베이스에 저장한다.
* 사용하는 테이블은 log이다.
* id는 자동으로 입력되도록 한다.

방명록 클래스 다이어그램

* 프레젠테이션(웹) 레이어 설정 파일 : web.xml, WebMvcContextConfiguration.java
* 서비스(비지니스), 레파지토리 레이어 설정 파일 : ApplicationConfig.java, DbConfig.java

* ![](/img/layerd1.png)
  * 설정 파일이 위의 그림처럼 4개가 필요하다.
  * web.xml에서는 두 개의 자바 config 파일에 대해 설정한다. 하나는 DispatcherServlet이 읽어들이는 WebMvcContextConfiguration이고, 또 하나는 ApplicationContextListener가 읽어들일 ApplicationConfig 파일이다. ApplicationConfig 파일에서는 DBconfig를 import하게 된다.
* ![](/img/layerd2.png)
  * 방명록 앱 어플리케이션에서 url 요청을 처리하는 핸들러인 GuestbookController.
  * GuestbookController는 비즈니스 로직을 갖고 있는 서비스 객체를 사용하게 된다.
  * 해당 서비스 객체는 GuestbookService라는 인터페이스와 GuestbookServiceImpl이라고 하는 실제 구현 클래스로 구성을 하게 될 것이다.
  * GuestbookServiceImpl에서는 logDao와 GuestbookDao를 이용해서 비즈니스 로직을 수행한다. 비즈니스 로직은 하나의 트랜잭션 단위로 동작한다.
  * LogDao는 저장만 하고 나머지 작업들은 수행하지 않는다. 그렇기 때문에 별도로 sql은 필요가 없다. 
  * GuestbookDao에서는 여러 개의 sql작업을 수행하기 때문에 이 sql들은 GuestbookDaoSqls 파일에서 한 번에 관리한다.
  * LogDao와 GuestbookDao가 사용할 dto가 필요하다.
  * 뷰의 역할을 수행하기 위해서 list.jsp를 작성한다.
  * index.jsp는 리다이렉트하는 코드만 나오게 된다.



**실습코드**

WebMvcContextConfiguration.java

```java
package kr.or.connect.guestbook.config;

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
@ComponentScan(basePackages = { "kr.or.connect.guestbook.controller" })
public class WebMvcContextConfiguration extends WebMvcConfigurerAdapter{

    @Override
    public void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/css/**").addResourceLocations("/css/").setCachePeriod(31556926);
        registry.addResourceHandler("/img/**").addResourceLocations("/img/").setCachePeriod(31556926);
        registry.addResourceHandler("/js/**").addResourceLocations("/js/").setCachePeriod(31556926);
    }
 
    // default servlet handler를 사용하게 합니다.
    // 맵핑 정보가 없는 url 요청이 들어 왔을 때, 맵핑정보가 없는 url 요청은 Spring의 DefaultServletHttpRequestHandler가 처리하도록 해주게 하는 것.
    // 맵핑 정보가 없는 url 요청이 들어왔을 때 WAS의 default servlet이 static한 자원을 읽어서 보여줄 수 있게끔 해준다.
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer) {
        configurer.enable();
    }
   
    //특정 url에 대한 처리를 컨트롤러 클래스를 작성하지 않고 맵핑할 수 있도록 해준다.
    @Override
    public void addViewControllers(final ViewControllerRegistry registry) {
    		System.out.println("addViewControllers가 호출됩니다. ");
        registry.addViewController("/").setViewName("index");
    }
    
    //viewResolver가 알맞는 view를 찾게 해준다.
    @Bean
    public InternalResourceViewResolver getInternalResourceViewResolver() {
        InternalResourceViewResolver resolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".jsp");
        return resolver;
    }
}
```



DBConfig.java

```java
package kr.or.connect.guestbook.config;

import javax.sql.DataSource;

import org.apache.commons.dbcp2.BasicDataSource;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.datasource.DataSourceTransactionManager;
import org.springframework.transaction.PlatformTransactionManager;
import org.springframework.transaction.annotation.EnableTransactionManagement;
import org.springframework.transaction.annotation.TransactionManagementConfigurer;

@Configuration
//트랜잭션과 관련된 설정을 자동으로 해준다. 단, 사용자 간의 트랜잭션 처리를 위한 PlatformTransactionManager를 설정하기 위해서는 TransactionManagementConfigurer를 구현하고 annotationDrivenTransactionManager를 override해야한다. 해당 메서드에서 트랜잭션을 처리할 PlatformTransactionManager 객체를 반환하게 하면 된다. annotationDrivenTransactionManager에서 호출하는 transactionManager() 메서드는 리턴 타입이 PlatformTransactionManager인 것을 볼 수 있다.
@EnableTransactionManagement
public class DBConfig implements TransactionManagementConfigurer {
	private String driverClassName = "com.mysql.jdbc.Driver";

	private String url = "jdbc:mysql://localhost:3306/connectdb?useUnicode=true&characterEncoding=utf8";

	private String username = "connectuser";

	private String password = "connect123!@#";

	@Bean
	public DataSource dataSource() {
		BasicDataSource dataSource = new BasicDataSource();
		dataSource.setDriverClassName(driverClassName);
		dataSource.setUrl(url);
		dataSource.setUsername(username);
		dataSource.setPassword(password);
		return dataSource;
	}

	@Override
	public PlatformTransactionManager annotationDrivenTransactionManager() {
		return transactionManger();
	}

	@Bean
	public PlatformTransactionManager transactionManger() {
		return new DataSourceTransactionManager(dataSource());
	}
}
```



ApplicationConfig.java

```java
package kr.or.connect.guestbook.config;

import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Import;

@Configuration
//dao나 service에 구현되어 있는 컴포넌트들을 읽어오면 되므로 basePackages에다가 각각의 패키지를 지정하고 있는 것을 볼 수 있다.
@ComponentScan(basePackages = { "kr.or.connect.guestbook.dao",  "kr.or.connect.guestbook.service"})
//dao, service에서 DB에 관련된 작업을 수행할 때 필요한 DB설정 파일 import
@Import({ DBConfig.class })
public class ApplicationConfig {

}
```



web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app>

	<display-name>Spring JavaConfig Sample</display-name>
	<context-param>
		<param-name>contextClass</param-name>
		<param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext
		</param-value>
	</context-param>
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>kr.or.connect.guestbook.config.ApplicationConfig
		</param-value>
	</context-param>
    <!-- 레이어드 아키텍쳐에 따라 설정 파일이 나눠진 상태이다. ApplicationConfig, DBConfig를 읽게 하기 위해 필요한 부분이다. listener는 어떤 특정한 이벤트가 일어났을 때 동작하는 것이다. ContextLoaderListener는 run on server를 하면 서버 실행을 위해 로딩이 되는데, 이처럼 Context가 로딩되는 이벤트가 발생했을 때 수행되는 리스너이다. 즉, Context가 로딩되면 ContextLoaderListener 클래스를 실행한다. 이 때, context-param에 등록되어 있는 부분들을 참고하게 된다. 따라서 ApplicationConfig와 DBConfig를 context-param이 등록해놓고 이벤트가 발생했을 때 리스터가 실행되면서 참고하게 된다.  -->
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener
		</listener-class>
	</listener>

	<servlet>
        <!-- 2. 받은 요청은 DispatcherServlet이 처리하게 하기위해 프론트 서블릿으로 등록한다. DispatcherServlet 클래스가 실행될 때 init-param으로 등록되어 있는 ApplicationConfig와 DBConfig를 가져다가 사용한다. -->
		<servlet-name>mvc</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet
		</servlet-class>
		<init-param>
			<param-name>contextClass</param-name>
			<param-value>org.springframework.web.context.support.AnnotationConfigWebApplicationContext
			</param-value>
		</init-param>
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>kr.or.connect.guestbook.config.WebMvcContextConfiguration
			</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
    <!-- 1. 모든 요청을 받는다. -->
	<servlet-mapping>
		<servlet-name>mvc</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>

    <!--filter는 요청이 수행되기 전, 응답이 나가기 전에 한 번씩 수행을 하게 되는 부분이다. spring이 제공하는 CharacterEncodingFilter를 등록해서 한글 인코딩 처리를 지원한다. 다른 값들은 다 정해져 있고, 우리가 지정할 수 있는 부분은 param-value의 인코딩 형식 뿐이다.-->
	<filter>
		<filter-name>encodingFilter</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter
		</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>encodingFilter</filter-name>
        <!--url pattern은 이 filter를 어디까지 적용하게 할 건지에 대한 부분이다. 모든 요청에 대해 지정을 하고 싶었기 때문에 /*로 지정을 한 것. 특정한 URL에만 지정할 수도 있다.-->
		<url-pattern>/*</url-pattern>
	</filter-mapping>
</web-app>
```



index.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<% 
	//list라는 요청으로 redirect한다.
	response.sendRedirect("list");
%>
```



**실습코드**

Guestbook.java

```java
package kr.or.connect.guestbook.dto;

import java.util.Date;

public class Guestbook {
	private Long id;
	private String name;
	private String content;
	private Date regdate;
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getContent() {
		return content;
	}
	public void setContent(String content) {
		this.content = content;
	}
	public Date getRegdate() {
		return regdate;
	}
	public void setRegdate(Date regdate) {
		this.regdate = regdate;
	}
	@Override
	public String toString() {
		return "Guestbook [id=" + id + ", name=" + name + ", content=" + content + ", regdate=" + regdate + "]";
	}
}
```



Log.java

```java
package kr.or.connect.guestbook.dto;

import java.util.Date;

public class Log {
	private Long id;
	private String ip;
	private String method;
	private Date regdate;
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getIp() {
		return ip;
	}
	public void setIp(String ip) {
		this.ip = ip;
	}
	public String getMethod() {
		return method;
	}
	public void setMethod(String method) {
		this.method = method;
	}
	public Date getRegdate() {
		return regdate;
	}
	public void setRegdate(Date regdate) {
		this.regdate = regdate;
	}
	@Override
	public String toString() {
		return "Log [id=" + id + ", ip=" + ip + ", method=" + method + ", regdate=" + regdate + "]";
	}
}
```



LogDao.java

```java
package kr.or.connect.guestbook.dao;

import javax.sql.DataSource;

import org.springframework.jdbc.core.namedparam.BeanPropertySqlParameterSource;
import org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate;
import org.springframework.jdbc.core.namedparam.SqlParameterSource;
import org.springframework.jdbc.core.simple.SimpleJdbcInsert;
import org.springframework.stereotype.Repository;

import kr.or.connect.guestbook.dto.Log;

@Repository
public class LogDao {
	private NamedParameterJdbcTemplate jdbc;
    private SimpleJdbcInsert insertAction;

    public LogDao(DataSource dataSource) {
        this.jdbc = new NamedParameterJdbcTemplate(dataSource);
        this.insertAction = new SimpleJdbcInsert(dataSource)
                .withTableName("log")
	            //id컬럼 값이 자동으로 입력되도록 하는 부분
                .usingGeneratedKeyColumns("id");
    }

	public Long insert(Log log) {
		SqlParameterSource params = new BeanPropertySqlParameterSource(log);
		return insertAction.executeAndReturnKey(params).longValue(); //executeAndReutrnKey() 메서드를 통해 insert문은 내부적으로 생성해서 실행을 하고 자동으로 생성된 id 값을 리턴하게 된다. 이 때 리턴 된 id 값을 사용할 수도 있다.
	}
}
```



GuestbookDaoSqls.java

```java
package kr.or.connect.guestbook.dao;

public class GuestbookDaoSqls {
    //mysql query 중에 limit를 이용하면 시작 값, 끝날 때의 값 등을 설정해서 특정한 부분만 select해오는 쿼리를 실행할 수 있다.
	public static final String SELECT_PAGING = "SELECT id, name, content, regdate FROM guestbook ORDER BY id DESC limit :start, :limit";
	public static final String DELETE_BY_ID = "DELETE FROM guestbook WHERE id = :id";
	public static final String SELECT_COUNT = "SELECT count(*) FROM guestbook";
}
```



GuestbookDao.java

```java
package kr.or.connect.guestbook.dao;

import java.util.Collections;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.sql.DataSource;

import org.springframework.jdbc.core.BeanPropertyRowMapper;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.jdbc.core.namedparam.BeanPropertySqlParameterSource;
import org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate;
import org.springframework.jdbc.core.namedparam.SqlParameterSource;
import org.springframework.jdbc.core.simple.SimpleJdbcInsert;
import org.springframework.stereotype.Repository;

import kr.or.connect.guestbook.dto.Guestbook;

import static kr.or.connect.guestbook.dao.GuestbookDaoSqls.*;

@Repository
public class GuestbookDao {
	 private NamedParameterJdbcTemplate jdbc;
	    private SimpleJdbcInsert insertAction;
	    private RowMapper<Guestbook> rowMapper = BeanPropertyRowMapper.newInstance(Guestbook.class);

	    public GuestbookDao(DataSource dataSource) {
	        this.jdbc = new NamedParameterJdbcTemplate(dataSource);
	        this.insertAction = new SimpleJdbcInsert(dataSource)
	                .withTableName("guestbook")
	                .usingGeneratedKeyColumns("id");
	    }
	    
	    public List<Guestbook> selectAll(Integer start, Integer limit) {
	    		Map<String, Integer> params = new HashMap<>();
	    		params.put("start", start);
	    		params.put("limit", limit);
	        return jdbc.query(SELECT_PAGING, params, rowMapper);
	    }


		public Long insert(Guestbook guestbook) {
			SqlParameterSource params = new BeanPropertySqlParameterSource(guestbook);
			return insertAction.executeAndReturnKey(params).longValue();
		}
		
		public int deleteById(Long id) {
			Map<String, ?> params = Collections.singletonMap("id", id);
			return jdbc.update(DELETE_BY_ID, params);
		}
		
		public int selectCount() {
			return jdbc.queryForObject(SELECT_COUNT, Collections.emptyMap(), Integer.class);
		}
}
```



GuestbookDaoTest.java

```java
package kr.or.connect.guestbook.dao;

import java.util.Date;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import kr.or.connect.guestbook.config.ApplicationConfig;
import kr.or.connect.guestbook.dto.Log;

public class GuestbookDaoTest {

	public static void main(String[] args) {
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig.class); 
//		GuestbookDao guestbookDao = ac.getBean(GuestbookDao.class);
//		
//		Guestbook guestbook = new Guestbook();
//		guestbook.setName("강경미");
//		guestbook.setContent("반갑습니다. 여러분.");
//		guestbook.setRegdate(new Date());
//		Long id = guestbookDao.insert(guestbook);
//		System.out.println("id : " + id);
		
		LogDao logDao = ac.getBean(LogDao.class);
		Log log = new Log();
		log.setIp("127.0.0.1");
		log.setMethod("insert");
		log.setRegdate(new Date());
		logDao.insert(log);
	}

}
```



**실습코드**

인터페이스가 들어갈 service 패키지와 이 service를 구현할 serviceImpl패키지를 만든다. 그리고 service안에 GuestbookService 인터페이스를 만들고, 어떤 비즈니스 메서드가 들어갈 지 생각해서 넣는다.

* 방명록 정보를 페이지 별로 읽어오기
* 페이징 처리를 위해서 전체 건 수 구하기
* 방명록 저장하기 

등을 생각해볼 수 있다.

GuestbookService.java

```java
package kr.or.connect.guestbook.service;

import java.util.List;

import kr.or.connect.guestbook.dto.Guestbook;

public interface GuestbookService {
    //페이지 당 보여지는 방명록의 숫자 나중에 이 부분만 수정하면 페이지당 보여지는 방명록 숫자를 한 번에 수정할 수 있다.
	public static final Integer LIMIT = 5;
    //조회
	public List<Guestbook> getGuestbooks(Integer start);
    //삭제 - ip는 LogDao를 통해 Log 테이블에 저장될 것이다.
	public int deleteGuestbook(Long id, String ip);
    //등록 - ip는 LogDao를 통해 Log 테이블에 저장될 것이다.
	public Guestbook addGuestbook(Guestbook guestbook, String ip);
    //개수 조회
	public int getCount();
}
```



GuestbookServiceImpl.java

```java
package kr.or.connect.guestbook.service.impl;

import java.util.Date;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import kr.or.connect.guestbook.dao.GuestbookDao;
import kr.or.connect.guestbook.dao.LogDao;
import kr.or.connect.guestbook.dto.Guestbook;
import kr.or.connect.guestbook.dto.Log;
import kr.or.connect.guestbook.service.GuestbookService;

//DAO는 @Repository라는 어노테이션을 붙여줬다면 서비스 쪽에다가는 @Service라는 어노테이션을 붙여주면 된다.
@Service
public class GuestbookServiceImpl implements GuestbookService{
    
    //자동으로 Bean을 등록해준다.
	@Autowired
	GuestbookDao guestbookDao;
	
	@Autowired
	LogDao logDao;

	@Override
    //읽기만 하는 메서드는 Transactional annotation을 붙여주면 내부적으로 readOnly라는 형태로 커넥션을 사용하게 된다.
	@Transactional
    //start부터 몇 개를 불러올지를 알아야하기 때문에 start를 인자로 받는다.
	public List<Guestbook> getGuestbooks(Integer start) {
		List<Guestbook> list = guestbookDao.selectAll(start, GuestbookService.LIMIT);
		return list;
	}

	@Override
    //readonly로 수행되면 안 되므로 false로 옵션 지정
	@Transactional(readOnly=false)
	public int deleteGuestbook(Long id, String ip) {
		int deleteCount = guestbookDao.deleteById(id);
		Log log = new Log();
		log.setIp(ip);
		log.setMethod("delete");
		log.setRegdate(new Date());
		logDao.insert(log);
		return deleteCount;
	}

	@Override
	@Transactional(readOnly=false)
    //geustbook 정보는 앞에 컨트롤러 단에서 넘겨 줬을 것이다. 컨트롤러 단에서는 클라이언트한테 받아온 정보들을 담고 있었을 것이다.
	public Guestbook addGuestbook(Guestbook guestbook, String ip) {
		guestbook.setRegdate(new Date());
        //insert 메서드가 수행됐을 때 id값을 리턴한다고 했으므로 받아서 저장
		Long id = guestbookDao.insert(guestbook);
		guestbook.setId(id);
		
//      트랜잭션 확인을 위해 일부러 exception을 수행시켜보는 부분  
//		if(1 == 1)
//			throw new RuntimeException("test exception");
//			
        //로그 부분에서 에러가 났는데, 앞에 수행된 부분이 취소가 되었다. 이것이 바로 트랜잭션.
		Log log = new Log();
		log.setIp(ip);
		log.setMethod("insert");
		log.setRegdate(new Date());
		logDao.insert(log);
		
		
		return guestbook;
	}

	@Override
    //페이징 처리를 위해서 전체 방명록 수를 구하는 부분
	public int getCount() {
		return guestbookDao.selectCount();
	}
	
	
}
```



GuestbookServiceTest.java

```java
package kr.or.connect.guestbook.service.impl;

import java.util.Date;

import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import kr.or.connect.guestbook.config.ApplicationConfig;
import kr.or.connect.guestbook.dto.Guestbook;
import kr.or.connect.guestbook.service.GuestbookService;

public class GuestbookServiceTest {

	public static void main(String[] args) {
		ApplicationContext ac = new AnnotationConfigApplicationContext(ApplicationConfig.class); 
		GuestbookService guestbookService = ac.getBean(GuestbookService.class);
		
		Guestbook guestbook = new Guestbook();
		guestbook.setName("kang kyungmi22");
		guestbook.setContent("반갑습니다. 여러분. 여러분이 재미있게 공부하고 계셨음 정말 좋겠네요^^22");
		guestbook.setRegdate(new Date());
		Guestbook result = guestbookService.addGuestbook(guestbook, "127.0.0.1");
		System.out.println(result);
		
	}

}
```

org.springframework.beans.factory.NoSuchBeanDefinitionException: No qualifying bean of type 'kr.or.connect.guestbook.serviceImpl.GuestbookServiceImpl' available

위의 오류 해결

https://stackoverflow.com/questions/26095881/no-found-for-dependency-expected-at-least-1-bean-which-qualifies-as-autowire-ca



mysql syntax-highlighting

https://github.com/dbcli/mycli



**실습코드**

GuestbookController.java

```java
package kr.or.connect.guestbook.controller;

import java.util.ArrayList;
import java.util.List;

import javax.servlet.http.HttpServletRequest;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

import kr.or.connect.guestbook.dto.Guestbook;
import kr.or.connect.guestbook.service.GuestbookService;

@Controller
public class GuestbookController {
    //service를 이용하기 위해서 autowired선언
	@Autowired
	GuestbookService guestbookService;
	
	@GetMapping(path="/list")
    //RequestParam으로 name이 start인 값을 받는데, 만약 start에 값이 없다면 기본 값을 0으로 주겠다 index가 0부터 시작하게 하기 위한 옵션.
	public String list(@RequestParam(name="start", required=false, defaultValue="0") int start,
					   ModelMap model) {
		
		// service로부터 start로 시작하는 방명록 목록 구해오기
		List<Guestbook> list = guestbookService.getGuestbooks(start);
		
		// 전체 페이지수 구하기
		int count = guestbookService.getCount();
        // 한 페이지당 보여줄 방명록 수
		int pageCount = count / GuestbookService.LIMIT;
		if(count % GuestbookService.LIMIT > 0)
			pageCount++;
		
		// 페이지 수만큼 start의 값을 리스트로 저장
		// 예를 들면 페이지수가 3이면
		// 0, 5, 10 이렇게 저장된다.
		// list?start=0 , list?start=5, list?start=10 으로 링크가 걸린다.
		List<Integer> pageStartList = new ArrayList<>();
		for(int i = 0; i < pageCount; i++) {
			pageStartList.add(i * GuestbookService.LIMIT);
		}
		
		model.addAttribute("list", list);
		model.addAttribute("count", count);
		model.addAttribute("pageStartList", pageStartList);
		
		return "list";
	}
	
	@PostMapping(path="/write")
	public String write(@ModelAttribute Guestbook guestbook,
						HttpServletRequest request) {
		String clientIp = request.getRemoteAddr();
		System.out.println("clientIp : " + clientIp);
		guestbookService.addGuestbook(guestbook, clientIp);
		return "redirect:list";
	}
}
```



list.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!-- jstl 사용을 위한 부분 -->
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>방명록 목록</title>
</head>
<body>

	<h1>방명록</h1>
	<br> 방명록 전체 수 : ${count }
	<br>
	<br>

	<c:forEach items="${list}" var="guestbook">

${guestbook.id }<br>
${guestbook.name }<br>
${guestbook.content }<br>
${guestbook.regdate }<br>

	</c:forEach>
	<br>

	<c:forEach items="${pageStartList}" var="pageIndex" varStatus="status">
		<a href="list?start=${pageIndex}">${status.index +1 }</a>&nbsp; &nbsp;
</c:forEach>

	<br>
	<br>
	<form method="post" action="write">
		name : <input type="text" name="name"><br>
		<textarea name="content" cols="60" rows="6"></textarea>
		<br> <input type="submit" value="등록">
	</form>
</body>
</html>
```





------

**생각해보기**

1. 레이어 별로 개발을 진행할 때, 각 레이어별로 잘 동작하는지 확인하는 것은 매우 중요합니다. 어떤 특정 레이어가 올바르게 동작하지 않는다면 웹 어플리케이션은 제대로 동작하지 않을 것입니다. 어느 특정 레이어가 문제가 있는지 알려면, 각 레이어별로 테스트가 필요합니다. 자바에서 테스트 코드를 좀 더 효과적으로 작성할 수 있는 방법에 대해 알아보세요.

 

 

------

**참고 자료**

- **[참고링크] Web on Servlet Stack**<https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html>


- **[참고링크] Serving Web Content with Spring MVC**<https://spring.io/guides/gs/serving-web-content/>


- **[참고링크] Spring MVC Tutorial**<https://www.javatpoint.com/spring-3-mvc-tutorial>