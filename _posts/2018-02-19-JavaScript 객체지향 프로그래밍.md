---
layout: post
title: JavaScript 객체지향 프로그래밍 
excerpt: "원시 타입과 참조 타입"
categories: [JavaScriptES5]
link:
comments: true
pinned: true
image:
  feature:

---



참고 자료 : 객체지향 자바스크립트의 원리 - 니콜라스 C.자카스 / 김태곤 역 



# 소개

* 객체 지향 언어의 특징
  * 캡슐화(Encapsulation) : 데이터와 데이터를 다루는 기능은 한 그룹으로 묶을 수 있다. 단순하게 말하면 이것이 객체의 정의이다.
  * 집합(Aggregation) : 한 객체는 다른 객체를 참조할 수 있다.
  * 상속(Inheritance) : 새로 생성된 객체는 다른 객체의 특성을 명시적으로 복제하지 않아도 다른 객체의 특성을 가진다.
  * 다형성(Polymorphism) : 여러 객체에서 같은 인터페이스를 구현할 수 있다.
* 자바 스크립트에는 클래스가 없지만 위의 4가지 특성은 모두 가지고 있으며, 의외의 방식으로 구성되어 있다.
* 타입 제약이 약하다는 자바스크립트의 특성을 활용하면 같은 작업을 위해 작성해야 할 코드가 다른 언어보다 더 적다. 나중에 필요한 클래스에 대해 고민하지 않고 바로 코딩을 시작할 수 있다. 특정 프로퍼티를 지닌 객체가 필요하다면? 원할 때 바로 만들어 쓰면 된다. 객체에 추가해야 할 메소드를 빠트렸다면? 나중에 추가하면 된다.



# 목차

1. 원시 타입과 참조 타입 : 자바스크립트에 존재하는 두 종류의 타입, 원시 타입과 참조 타입에 대해 다룬다. 두 타입의 차이를 아는 것이 중요하다.
2. 함수 : 함수의 입출력에 대해 다룬다. 자바스크립트는 일급 함수에 대한 개념을 알아야 한다.
3. 객체의 이해 : 자바스크립트의 객체 구조를 설명한다. 자바스크립트의 객체는 다른 언어의 객체와 다르게 동작하므로 객체의 동작원리를 잘 이해하고 있어야 한다.
4. 생성자와 프로토타입 : 생성자에 대해 살펴보며 함수에 대해 배웠던 내용을 심화 학습한다. 모든 생성자는 함수이지만 일반적인 함수와는 사용법이 다르다. 두 방식의 차이점을 살펴보고, 고유 타입을 작성하는 법을 배운다.
5. 상속 : 자바 스크립트에서 상속이 이루어지는 방식을 설명한다. 자바스크립트에 클래스가 없지만 상속을 할 수 없는 것은 아니다. 프로토타입 상속을 배우고 프로토타입 상속과 클래스 기반 상속의 차이점에 대해 알아본다.
6. 객체 패턴 : 자주 사용되는 객체 패턴을 살펴본다. 자바스크립트에서는 여러 방법으로 객체를 작성하고 구성할 수 있다. 이 장에서는 그 중 가장 유명한 패턴 몇 가지를 살펴본다.



1. # 원시 타입과 참조 타입

자바스크립트는 언어의 중심을 객체에 두고 있다. 자바스크립트에서 데이터 대부분은 객체이거나 객체를 통해 접근하는 값이다. 자바스크립트는 함수조차 객체로 표현하며 덕분에 자바스크립트의 함수는 **일급 함수(first-class functions)**이다.



### 타입이란?

클래스라는 개념을 대체할 타입이라는 개념이 존재하며, 타입은 크게 원시 타입과 참조타입 두 종류로 나뉜다. 

---

### 리터럴 형식

들어가기 전에, 리터럴 형식이 무엇인지에 대해 파악할 필요가 있다.

- 리터럴 형식 : 값을 표현하는 방식

  - 리터럴(literal) : 코드에 직접 입력된 이름이나 가격처럼 변수에 저장되지 않은 값

  - ```javascript
    //문자열
    var name = "Nicolas";
    var selection = "a";

    //숫자
    var count = 25;
    var cost = 1.51;

    //불리언
    var found = true;

    //null
    var object = null;

    //undefined
    var flag = undefined;
    var ref ; // 자동으로 undefined가 할당됨.
    ```

---

### 원시 타입

* 원시 타입 : 단순한 데이터를 저장

  * Boolean(불리언) : true/false

  * Number(숫자) : 정수 또는 부동소수점 실수 값

  * String(문자열) : 한 쌍의 작은 따옴표 또는 큰 따옴표로 감싼 일련의 문자(자바스크립트에는 문자 타입이 따로 없다.)

  * Null : null이라는 값만 있는 원시 타입

  * Undefined : undefined라는 값만 있는 타입 (undefined는 아무런 값도 할당되지 않은 변수에 할당되는 값)

  * 원시 타입의 복사(값 자체가 저장된다.)

    * ~~~javascript
      var color1 = "red";
      var color2 = color1;
      ~~~

  * 원시 타입의 종류 확인 (typeof 연산자 사용. null은 '===' 사용)

    * ~~~javascript
      console.log(typeof "Nicolas"); //"String"
      console.log(typeof 10); //"number"
      console.log(typeof 5.1); //"number"
      console.log(typeof true); //"boolean"
      console.log(typeof undefined); //"undefined"

      console.log(typeof null); //"object" -> 이 부분은 TC39 위원회에서 실수라고 인정 
      console.log(value === null); //true 또는 false
      ~~~

  * '=='와 '==='의 차이 

    * == : 비교 수행 전에 자동 형 변환 실행 후 비교

    * === : 비교 수행 전에 자동 형 변환을 실행하지 않고 비교

    * ~~~javascript
      console.log("5" == 5); // true
      console.log("5" === 5); // false

      console.log(undefined == null); //true
      console.log(undefiend === null); //false
      ~~~

  * 원시 메소드

    * 문자열, 숫자, 불리언에는 메소드가 존재한다.(null, undefined는 메소드가 없다.)
      * String method : https://www.w3schools.com/js/js_string_methods.asp
      * Number method : https://www.w3schools.com/js/js_number_methods.asp
      * Boolean method : https://www.w3schools.com/js/js_booleans.asp


---

### 참조 타입

* 참조 타입 : 객체로서 저장(메모리상의 주소를 가리킨다.). 자바스크립트 객체를 나타내며 클래스와 가장 가까운 개념.

  * 참조 값 : 참조 타입의 인스턴스(instance). 객체(objects)와 같은 말. 객체는 순서가 없는 프로퍼티(property로 구성)
  * 프로퍼티(property) : 이름(문자열)과 값으로 구성되어 있다.
  * 메소드(method) : 프로퍼티의 값이 함수 일 때 해당 프로퍼티

* 객체 생성(객체 참조 생성)

  * 인스턴스 화(instantiate) : 객체를 만드는 것. 자바스크립트에는 객체 생성을 하는 두 가지 방법이 있다. 

    1. new 연산자와 생성자를 사용 : 관례상 생성자는 대문자로 시작하여 생성자가 아닌 함수와 구분 한다.

       * ~~~javascript
         var object = new Object(); // 일반 객체(generic obejct)를 하나 작성하고 객체의 참조(값을 가리키는 메모리 주소)를 object변수에 저장
         ~~~

       * 이 때, object에 저장된 값은 사실 객체 인스턴스가 아니라 객체가 있는 메모리 상의 위치를 가리키는 포인터(또는 참조)이다. 이것이 바로 객체와 원시 값의 가장 큰 차이점이다. 원시 값은 변수에 직접 값 자체가 저장된다.

       * ~~~javascript
         var object1 = new Object(); //새로운 객체 생성 후, 참조 값을 object1에 할당
         var object2 = object1; //object1에 저장된 참조 값을 object2에 할당
         ~~~

       * 이 때, object1과 object2는 같은 객체를 가리키는 포인터이다.

    2. 객체 리터럴 방식 사용

       * ~~~javascript
         var object = {};
         ~~~

    3. <u>생성자, 객체 리터럴 방식의 차이</u>

       1. 생성자 함수로 생성된 객체(인스턴스)는 자신의 프로토타입으로 생성자 함수의 프로토타입 프로퍼티가 가리키는 프로토타입 객체를 참조한다.
       2. 반면, 객체 리터럴로 생성된 객체(인스턴스)는 자신의 프로토타입으로 Object를 참조한다.

* 객체 참조 제거

  * 자바스크립트는 가비지 컬렉션 기능이 있는 언어이므로 참조 타입을 사용할 때 메모리 할당에 대해 고민하지 않아도 된다. 하지만 가비지 컬렉터가 메모리를 해제할 수 있도록 사용하지 않는 객체에 대해서는 참조 제거를 해두는 편이 좋다.

  * 가비지 컬렉션(garbage collection) : 동적으로 할당된 메모리 블럭이나 객체 중 더 이상 사용하지 않는 것을 제거하여 사용할 수 있는 메모리로 만드는 기능

  * 가비지 컬렉터(garbage collerctor) : 프로그래밍 언어에서 가비지 컬렉션을 수행하는 부분.

  * ~~~javascript
    var object1 = new Ojbect();
    //실행할 코드
    object1 = null; // 참조 제거
    ~~~

  * 객체를 수백만 개씩 사용하는 대규모 어플리케이션에서는 객체의 참조 제거가 특히 중요하다

* 프로퍼티 추가 및 제거

  * ~~~javascript
    var object1 = new Object();
    var object2 = object1;

    object1.myCustomProperty = "Awesome!";
    console.log(object2.myCustomProperty); //"Awesome!"
    ~~~

---

### 내장 참조 타입

(Object 타입 외 JavaScript에서 기본적으로 제공하는 유용한 내장 참조 타입)

* 종류
  * Array : 숫자 인덱스 값을 가진 순차 목록
  * Date : 날짜와 시간
  * Error : 실행 중 발생하는 에러 (에러의 종류에 따라 더 구체적인 하위 에러 타입이 존재한다.)
  * Function : 함수
  * Object : 일반적인 객체
  * RegExp : 정규 표현식

* 내장 참조 타입 인스턴스화

  * ~~~javascript
    var items = new Array();
    var now = new Date();
    var error = new Error("에러가 발생했습니다.");
    var func = new Function("console.log('Hi');");
    var object = new Object();
    var re = new RegExp("\\d+");
    ~~~

* 리터럴 형식

  * 일부 내장 참조 타입은 리터럴 형식 사용 가능 : new 연산자와 객체의 생성자를 사용하여 명시적으로 객체를 만들지 않고도 참조 값을 만들 수 있다.(원시 값 리터럴에 new 연산자가 필요 없는 것과 같다.)

    * 객체 및 배열 리터럴

      * ~~~javascript
        var book = {
            name : "객체지향 자바스크립트의 원리",
            year : 2014
        };

        var book = {
            "name" : "객체지향 자바스크립트의 원리",
            "year" : 2014
        }; // 프로퍼티 이름을 문자열 리터럴로 만들면 공백과 같은 특수 문자도 사용 가능.
        ~~~

      * 위 방식은 아래 코드와 동일하다.

        ~~~javascript
        var book = new Object();
        book.name = "객체지향 자바스크립트의 원리";
        book.year = 2014;
        ~~~

    * 배열 리터럴

      * ~~~javascript
        var colors = ["red", "blue", "green"];
        console.log(colors[0]); //"red"
        ~~~

      * 위 방식은 아래 코드와 동일하다.

        ~~~javascript
        var colors = new Array("red", "blue", "green")
        console.log(colors[0]); //"red"
        ~~~

    * 함수 리터럴

      * 함수는 보통 리터럴 형식을 사용해 정의된다.

      * ~~~javascript
        function reflect(value){
            return value;
        }
        ~~~

      * 위 방식은 아래 코드와 동일하다.

        ~~~javascript
        var reflect = new Function("value", "return value;");
        //생성자 함수 정의 방식은 가독성이 떨어지고 디버그가 어려우므로 사용 빈도가 낮다.
        ~~~

    * 정규 표현식 리터럴

      * RegExp생성자를 사용하지 않고 정규표현식을 정의할 수 있다.

      * ~~~javascript
        var numbers = /\d+/g; //문자열 안에 있는 문자를 어떻게 이스케이프 해야 할지 고민 할 필요가 없어 코드 작성이 훨씬 수월하다.
        ~~~

      * 위 방식은 아래 코드와 동일하다.

        ~~~javascript
        var numbers = new RegExp("\\d+","g");
        ~~~

        ​