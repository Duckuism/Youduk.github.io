---
layout: post
title: MySQL mac os 설정 방법 및 에러
excerpt: "참고 자료와 정리"
categories: [SQL]
link:
comments: true
pinned: true
image:
  feature:
---


<h5>how to start mysql server in mac os</h5>

https://github.com/helloheesu/SecretlyGreatly/wiki/%EB%A7%A5%EC%97%90%EC%84%9C-mysql-%EC%84%A4%EC%B9%98-%ED%9B%84-%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0

<h5>맥 터미널에서 mysql실행하기</h5>

https://stackoverflow.com/questions/26554818/using-mysql-in-the-command-line-in-osx-command-not-found

<h5>The server quit without updating PID file 에러.</h5>

https://bryan7.tistory.com/476

https://bellsilver7.tistory.com/28

https://stackoverflow.com/questions/9624774/after-mysql-install-via-brew-i-get-the-error-the-server-quit-without-updating

https://stackoverflow.com/questions/4444861/pid-error-on-mysql-server-start

<br />
해결방법이 약간 서로 다른데; 세번째가 가장 자세하다.

위에 질문들을 통해 mysql을 homebrew로 설치하고, 경로를 설정했다.

그리고 최종으로는 공식 홈페이지의 방법으로 command line client로 접속할 수 있었다.<br />

https://dev.mysql.com/doc/mysql-getting-started/en/#mysql-getting-started-connecting <br />

<h5>mysql 캐릭터셋 바꾸는 명령어.</h5>

https://develop.sunshiny.co.kr/385

set character_set_server = utf8;<br />



<h5>No mapping found for HTTP request with URI 에러</h5>

https://acua.tistory.com/entry/No-mapping-found-for-HTTP-request-with-URI <br />

위의 이유는 아니었고 root-context.xml에서 base-package가 내가 원하는 패키지로 설정이 안되어서 일어난 경우도 있었다.

<h5> Page directive: illegal to have multiple occurrences of 'contentType' with different values 에러 </h5>

https://namsieon.com/16

<h5>STS, 이클립스 설정 메모리 늘리기</h5>

https://skycow79.tistory.com/26

https://doublesprogramming.tistory.com/15

<h5>이클립스 메모리 설정과 초기 설정 팁<h5>

https://alnet.tistory.com/14

<h5>Caught exception while allowing TestExecutionListener 에러</h5>

https://github.com/slippStudy/passion/issues/27

https://jellyms.kr/105
아래 방법으로 해결


<h5>myBatis에러</h5>

https://kr-zephyr.github.io/java/mybatis/resolve-issue/2016/08/11/mybatis-mapped-statements-collection-does-not-contain-value.html



<h5>fail to load applicationContext 에러</h5>

https://lks21c.blogspot.kr/2011/12/junit-fail-to-load-applicationcontext.html

이건 결국 설정 문제

WARN : org.springframework.web.servlet.PageNotFound - No mapping found for HTTP request with URI [/replies] in DispatcherServlet with name 'appServlet'

org.springframework.beans.factory.UnsatisfiedDependencyException
org.springframework.beans.factory.NoSuchBeanDefinitionException

root-context.xml에 sqlSessionFactory beans를 추가해주지 않아서 생기는 문제였다.
<br />
https://stackoverflow.com/questions/18001600/caused-by-org-springframework-beans-factory-nosuchbeandefinitionexception<br />
https://docs.spring.io/spring/docs/3.2.x/spring-framework-reference/htmlsingle/#orm-hibernate<br />

페이징 처리할 때 작업 순서(즉, 풀 작업 순서)

1. DAO(ReplyDAO)
2. XML Mapper(relyMapper.xml)
3. DAOImpl(ReplyDAOImpl)
4. Service(ReplyService)
5. ServiceImpl(ReplyServiceImpl)
6. Controller(ReplyController)

<h5>Uncaught TypeError: $ is not a function 에러</h5>

https://www.xetown.com/qna/146140

<h5>Uncaught TypeError: Cannot read property 'replace' of undefined</h5>

첫번쨰<script></script>안에 선언한 변수를 두 번째 <script></script>안에서 읽으려고 해서 나는 오류였다.


<sql 외래키 오류 해결 쿼리문>

foreign key 제약 조건 삭제
alter table tbl_reply drop foreign key fk_board;

제약 조건 외래키 및 on delete cascade 속성 추가 쿼리문
alter table tbl_reply add constraint fk_board
foreign key(bno) references tbl_board(bno)
on delete cascade;
