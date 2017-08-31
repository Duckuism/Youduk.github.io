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

참고도서의 내용을 바탕으로 나름대로 요약한 내용을 게시한다.

  1. 람다식이란?

람다식(Lambda expression)은 간단히 말해서 메서드를 하나의 '식(expression)'으로 표현한 것이다. 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로, 람다식을 '익명 함수(anonymous function)'이라고도 한다.

  2. 람다식 작성 방법

~~~java
1. 기존의 메서드
int max(int a, int b){
  return a>b ? a:b;
}

2. 람다식으로 변환
(int a, int b) -> {
  return a>b ? a:b;
}

3. 반환 값이 있는 메서드는 return문 대신 식으로 더 간결하게 표현 가능
(int a, int b) -> a>b? a:b

4. 람다식에 선언된 매개변수의 타입은 추론이 가능한 경우 생략 가능(대부분 가능)
(a,b) -> a>b ? a:b
~~~

  3. 함수형 인터페이스(Functional Interface)

함수형 인터페이스 : 람다식을 다루기 위한 인터페이스 (람다식과 1:1 대응이 필요하므로 하나의 추상 메서드만 정의되어 있어야 한다.)

이러한 함수형 인터페이스를 구현한 참조 변수를 가지고 람다식(익명 객체)의 메서드를 호출한다.

java.util.function 패키지에서는 자주 사용하는 형식의 함수형 인터페이스를 미리 정의해 놓았다. 이 패키지를 이용하면 일일히 메서드를 지정하지 않아도 된다.

>java.util.function
>* java.lang.Runnable
>* Supplier<T>
>* Consumer<T>
>* Funtion<T,R>
>* Predicate<T>

  4. 메서드 참조

람다식이 하나의 메서드만 호출하는 경우에는 '메서드 참조(method reference)'라는 방법으로 람다식을 간략히 할 수 있다.

~~~java

Funtion<String, Integer> f = (String s)
-> Integer.parseInt(s);
~~~

|  <center>종류</center> |  <center>람다</center>|<center>메서드 참조</center>|
|:--------|:--------|:--------|
|**static메서드 참조 방법** |(x)->ClassName.method(x)|ClassName::method|
|**인스턴스메서드 참조 방법** |(obj,x)->obj.method(x)|ClassName::method|
|**특정 객체 인스턴스메서드 참조** |(x)->obj.method(x)|obj::method|
|**생성자 호출 람다식(매개변수 x) 메서드 참조** |Supplier<MyClass> s = () -> new MyClass(); |Supplier<MyClass> s = MyClass::new|
|**생성자 호출 람다식(매개변수 o) 메서드 참조** |Function<Integer, myClass> f = (i) -> new MyClass(i); //람다식 <br /> Function<Integer, myClass> f2 = MyClass::new; //메서드 참조 <br /><br />BiFunction<Integer, String, myClass> bf = (i,s) -> new MyClass(i,s); //람다식 <br /> Function<Integer, String, myClass> bf2 = MyClass::new; //메서드 참조 <br />|
|**배열 생성 메서드 참조** |Function<Integer, int[]> f = x -> new int[x];|Function<Integer, int[]> f2 = int[]::new;|



~~~java
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
~~~
