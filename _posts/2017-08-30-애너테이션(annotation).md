---
layout: post
title: 애너테이션(annotation)
excerpt: ""
categories: [java]
link:
---
### 애너테이션
###### 참고도서 : 자바의 정석(남궁성 저, 도우출판)

* 흐름을 읽기 위한 단원 목차 훑기
  1. 애너테이션이란?
  2. 표준 애너테이션
  3. 메타 애너테이션
  4. 애너테이션 타입 정의하기(이 부분이 실제로 쓰는 부분)

수업 복습 내용

@Test(count=1,exception = "ClassCastException")

애너테이션의 멤버가 하나일 때는 생략가능

@Test(count=1)로 해야하지만

@Test(1);로 가능

@interface Text{
  int count
}

@Test(1);

@interface Text{
  int count default 1;
}

@Test; default가 있으면 이렇게 가능

@interface Text{
  int count default 1;
  String[] types;
}

@Test(types={"checked",rawtype});로 해야하지만
@test(); 이렇게 가능

@interface Text{
  int count default 1;
  String[] types default{"rawtype","unchecked"};
}
@Test; default가 있으면 이렇게 가능
