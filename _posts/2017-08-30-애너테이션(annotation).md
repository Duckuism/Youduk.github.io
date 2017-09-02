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

1. 애너테이션이란?

주석 안에 미리 정의된 태그들(@)을 이용해 정보를 저장하고 javadoc.exe 프로그램이 이 정보를 읽어서 문서를 작성하는 기능을 응용하여 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것. 애너테이션은 주석처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다는 장점이 있다.

2. 애너테이션 정리

|  <center>표준 애너테이션</center> |  <center>설명</center>|
|:--------|:--------|
|**@Override** |컴파일러에게 오버라이딩하는 메서드라는 것을 알린다.|
|**@deprecated** |앞으로 사용하지 않을 것을 권장하는 대상에 붙인다.|
|**@SuppressWarnings** |컴파일러의 특정 경고메시지가 나타나지 않게 해준다.|
|**@SafeVarargs** |지네릭스 타입의 가변인자에 사용한다.(JDK1.7)|
|**@FunctionalInterface** |함수형 인터페이스라는 것을 알린다.(JDK1.8)|
|**@Native** |native메서드에서 참조되는 상수 앞에 붙인다.(JDK1.8)|

|  <center>메타 애너테이션</center> |  <center>설명</center>|
|:--------|:--------|
|**@Target** |애너테이션이 적용가능한 대상을 지정하는데 사용한다.|
|**@Documented** |애너테이션 정보가 javadoc으로 작성된 문서에 포함되게 한다.|
|**@Inherited** |애너테이션이 자손 클래스에 상속되도록 한다.|
|**@Retention** |애너테이션이 유지되는 범위를 지정하는데 사용한다.|
|**@Repeatable** |애너테이션을 반복해서 적용할 수 있게 한다.(JDK1.8)|

* 메타 애너테이션(meta annotation) : 애너테이션의 애너테이션. 즉 애너테이션에 붙이는 애너테이션으로 애너테이션을 정의할 때 애너테이션의 적용대상(target)이나 유지기간(retention)등을 지정하는데 사용된다.

3. 애너테이션 타입 정의
직접 애너테이션을 만들 수 있다. '@'기호를 붙이는 것을 제외하면 인터페이스를 정의하는 것과 동일하다.

~~~java
@interface 애너테이션이름{
  타입 요소 이름(); // 애너테이션의 요소 선언.
}
~~~

* 애너테이션의 요소
애너테이션 내에 선언된 메서드를 애너테이션의 요소(element)라고 한다. 애너테이션의 요소는 반환값이 있고 매개변수는 없는 추상 메서드의 형태를 가지며, 상속을 통해 구현하지 않아도 된다. 다만, 애너테이션을 적용할 때 이 요소들의 값을 빠짐없이 지정해주어야 한다. 요소의 이름도 같이 적어주므로 순서는 상관 없다.

~~~java
//다섯개의 요소를 가진 애너테이션
@interface TestInfo{
  int count();
  String testedBy();
  String[] testTools();
  TestType testType(); // enum TestType {FIRST, FINAL}
  DateTime testDate(); // 자신이 아닌 다른 애너테이션(@DateTime)을 포함할수 있다.
}

@interface DateTime{
  String yymmdd();
  String hhmmss();
}

//애너테이션의 요소는 기본 값을 가질 수 있으며, 기본값이 있는 요소는 애너테이션을 적용할 때 값을 지정하지 않으면 기본값 사용(기본값은 null을 제외한 모든 리터럴이 가능)
@interface TestInfo {
  int count() default 1;
}
@TestInfo //@TestInfo(count = 1)과 동일
public class newClass{ }
~~~

4. 애너테이션 요소 선언 규칙
애너테이션의 요소를 선언할 때 반드시 지켜야 하는 규칙
```
* 요소의 타입은 기본형, String, enum, 애너테이션, Class만 허용된다.
* ()안에 매개변수를 선언할 수 없다.
* 예외를 선언할 수 없다.
* 요소를 타입 매개변수로 정의할 수 없다.
```

<h4>* 수업 복습내용</h4>

~~~java

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
~~~
