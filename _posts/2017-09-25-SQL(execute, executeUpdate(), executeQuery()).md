---
layout: post
title: SQL(execute, executeUpdate(), executeQuery())
excerpt: "execute, executeUpdate(), executeQuery()의 차이"
categories: [Servlet/JSP/Spring]
link:
comments: true
pinned: true
image:
  feature:
---

1.execute

- executeQuery, executeUpdate 두가지 모두의 경우를 모두 포함한다.

즉 DDL, DML, DCL 모두 사용할수 있다는 것이다.

다만, 리턴이 boolean 값으로 넘어온다.



2. executeQuery()

- ResultSet을 얻기 위한 메소드

- 주로 select 문이 이에 속한다.



3. executeUpdate()

- 적용된 행의 갯수를 얻기 위한 메소드

-DDL(insert, update, delete)에 사용된다.

-DML(crete, drop, alter)에 사용횐다.



출처: http://gangyup.tistory.com/entry/execute-executeQuery-executeUpdate-메소드의-차이점 [쁨엽이]
