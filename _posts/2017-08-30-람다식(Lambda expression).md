---
layout: post
title: 람다식(Lambda expression)
excerpt: ""
categories: [java]
link:
---
### 람다식
###### 참고도서 : 자바의 정석(남궁성 저, 도우출판)

* 흐름을 읽기 위한 단원 목차 훑기
  1. 람다식이란?
  2. 람다식 작성하기
  3. 함수형 인터페이스(Functional Interface)
  4. java.util.function 패키지
  5. Function의 합성과 Predicate의 결합
  6. 메서드 참조

수업 복습내용
//기존
int max(int a, int b){
  return a>b ? a:b
}
//1단계
(int a, int b)-> a>b? a:b;
//2단계
(a,b) -> a>b? a:b ;
(익명 객체기 떄문에 함수형 인터페이스에서 그냥 못쓴다.)
new Object(){
  int max(int a, int b){
    return a>b? a:b;
  }
}
이러한 익명 객체를 다루기 위한 참조 변수가 함수형 인터페이스인 것.

* 함수형 인터페이스 : 추상 메서드가 한 개인 인터페이스

왜 쓰냐? 람다식 다루려고, 참조하려고.

위의 것을 참조하려면

BiFunction <Integer,Integer,Integer> f=(int a,int b)->a>b? a:b; 실제로 주고받는 정보내용은 이렇지만 입출력 내용을 굳이 적어주지 않아도 되어서 아래처럼 생략하는 것.
BiFunction f=(a,b)->a>b? a:b;
여기서 f가 참조 변수고 이 참조 변수로 익명 객체를 다루는 것.
java.util.factory 패키지에 있으니까 만들기 보다는 갖다 쓸 것.

* 메서드 참조

메서드 한 개를 호출하는 람다식
예를들면

(String s) -> Integer.parseInt(S); 이경우에는 메서드 한개. 이 때 Integer::parseInt로 간단히 쓴다는 것.

(Object x, Object x) => o.equals(x); -> String::equals
(Object c) -> new String[] -> String::new
