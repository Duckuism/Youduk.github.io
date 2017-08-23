---
layout: post
title: 컬렉션 프레임워크 (collections framework)
excerpt: "표준화된 프로그래밍을 위해!"
categories: [java]
link: 

---

### 컬렉션 프레임워크에 대해

###### 참고 도서 : 자바의 정석(남궁성 저, 도우출판)

컬렉션 프레임워크란 데이터 군을 저장하는 클래스들을 표준화한 설계를 뜻한다. 컬렉션 프레임워크는 컬렉션(다수의 데이터)을 다루는 데 필요한 다양하고 풍부한 클래스들을 제공하기 떄문에 프로그래머에게 유용하며, 인터페이스와 다형성을 이용한 객체지향적 설계를 통해 표준화 되어 있기 때문에 사용법을 익히기에도 편리하다. 또한 재사용성이 높은 코드를 작성할 수 있다는 장점이 있다. 아래는 기본 개념의 정의이다.

> 컬렉션 프레임워크
1. 데이터 군을 저장하는 클래스들을 표준화한 설계
2. 다수의 데이터를 쉽게 처리할 수 있는 방법을 제공하는 클래스들로 구성
3. JDK1.2부터 제공

> 컬렉션
* 다수의 데이터 즉, 데이터 그룹을 의미한다.

> 프레임워크(framework)
* 표준화, 정형화된 체계적인 프로그래밍 방식

> 컬렉션 클래스(collection class)
* 다수의 데이터를 저장할 수 있는 클래스( e.g - Vector, ArrayList, HashSet)

1. 컬렉션 프레임 워크의 핵심 인터페이스

    |  <center>인터페이스</center> |  <center>특징</center> |
    |:--------|:--------|
    |**List** |순서가 있는 데이터의 집합. 데이터의 중복을 허용한다.|
    |**Set** |순서를 유지하지 않는 데이터의 집합. 데이터의 중복을 허용하지 않는다.|
    |**Map** |키(key)와 값(value)의 쌍(pair)으로 이루어진 데이터의 집합. 키 순서는 유지되지 않으며, 키는 중복을 허용하지 않고 값은 중복을 허용한다.|

    1.1 Collec
    
2. ArrayList
3. LinkedList
4. Stack과 Queue
5. Iterator, Listlterator, Enumeration
6. Arrays
7. Comparator / Comparable
8. HashSet
9. TreeSet
10. HashMap / Hashtable
11. TreeMap
12. Properties
13. Collections
14. 컬렉션 클래스 정리 및 요약






