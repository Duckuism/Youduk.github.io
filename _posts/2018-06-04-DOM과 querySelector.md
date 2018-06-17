---
layout: post
title: DOM
excerpt: "DOM과 querySelector"
tags: [Boostcourse]
categories: [WebFE]
link:
comments: true
pinned: true
image:
  feature:
---

## DOM과 qeurySelector

### **1. DOM**

브라우저에서는 HTML코드를 DOM(Document Object Model)이라는 객체형태의 모델로 저장한다. 

그렇게 저장된 정보를 DOM Tree라고 부른다.

결국 HTML element는 Tree 형태로 저장되는 것.

![](/Img/WebUI_5.png)

- **Dom tree**


복잡한 DOM Tree를 탐색하기 위해 JavaScript로 탐색알고리즘을 구현하면 너무 비용이 많이 든다.

그래서 브라우저에서는 DOM(document object model)이라는 개념을 통해서, 다양한 DOM API(함수 묶음정도)를 제공하고 있다.

브라우저는 DOM Tree찾고 조작하는 걸 쉽게 도와주는 여러 가지 메서드를(DOM API)를 제공한다.



#### **2. getElementById()**

ID 정보를 통해서 찾을 수 있다.

MDN사이트를 참고해서 이를 테스트해보도록 하자.

테스트를 할 때는 특정 웹사이트에 접속한 후, 크롬 개발자도구-콘솔을 열어서 그곳에서 코딩을 해보면서 간편하게 찾을 수 있다. 

~~~javascript
//DOM모델명.getElementById("아이디명");
document.getEelementById("nav-cart-count").style.display="block";
~~~



### **3. Element.querySelector()**

DOM을 찾는데 특히 유용한 querySelector 메서드.

CSS 스타일을 결정할 때 사용하던, Selector 문법을 활용해 DOM에 접근할 수 있다.

DOM을 찾을 때 querySelector만 써도 충분하다.
참고로, 비슷하지만 다른 querySelectorAll도 있다. 특정 선택자를 가진 요소들을 배열로 만들어서 반환하는 메서드이다.

~~~javascript
document.querySelector("div"); //div태그를 찾아준다.
document.querySelector("#nav-cart-count") //cssSelector를 이용해 태그 대신 id나 class를 찾을 수도 있다.
document.querySelector("body #nav-cart-count") //상속 관계 표현도 가능하다.
document.querySelector("#nav-cart-count > .nav-arrow") //상속 관계 표현도 가능하다.
~~~



### **4. css selector**

selector문법은 querySelector와 querySelectorAll메서드에서 사용할 수 있으며, css 스타일을 부여했을 때 익혔던 selector문법과 동일하다고 생각하고 사용할 수가 있다.

다양한 css selector문법을 사용해서 원하는 엘리먼트를 찾을 수 있다.

 