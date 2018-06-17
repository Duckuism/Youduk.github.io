---
layout: post
title: Event
excerpt: "event를 처리하는 방법"
tags: [Boostcourse]
categories: [WebFE]
link:
comments: true
pinned: true
image:
  feature:
---

## **Event**

브라우저에는 많은 이벤트가 발생한다.

브라우저 화면의 크기를 마우스로 조절할 때도, 스크롤을 할 때도, 마우스로 이동하거나 무언가를 선택할 때도 
이벤트가 발생한다.

이벤트를 브라우저가 발생시켜주니, 우리는 해당 이벤트가 일어날 때 어떤 일을 하라고 할 일을 등록할 수가 있다.

다시 말해, HTML엘리먼트별로 어떤 이벤트(주로 키보드나 마우스 관련)가 발생했을 때 특정 행위를(어떤 일) 하고 싶다면, 대상엘리먼트를 찾고 어떤 일을 등록하면 된다.

이걸 자바스크립트로 구현할 수 있다.



### **이벤트 등록**

이벤트를 등록하는 표준방법.

addEventListener 함수를 사용할 수 있다.

```javascript
var el = document.querySelector(".outside");

el.addEventListener("click", function(e){
	console.log("clicked!!", e);//이벤트 리스터에 매개변수로 이벤트 객체를 넣어서 이벤트 객체 속성들을 출력할 수도 있다.
}, false);
//el 객체에 클릭 이벤트가 일어나면 함수 안의 내용을 실행하라는 뜻이다. 이 실행 함수를 event handler 혹은 event listener라고 표현한다. 
```

addEventListener 함수의 두 번째 인자는 함수다.

이 함수는 나중에 이벤트가 발생할 때 실행되는 콜백 함수로 이벤트핸들러(Event Handler) 또는 이벤트리스너(Event Listener)라고 부른다.

콜백함수는 이벤트가 발생할 때 실행된다. 



### **이벤트 객체**

브라우저는 이벤트 리스너를 호출할 때, 사용자로부터 어떤 이벤트가 발생했는지에 대한 정보를 담은 이벤트 객체를 생성해서 리스너 함수에 전달합니다.

따라서 이벤트리스너 안에서는 이벤트객체를 활용해서 추가적인 작업을 할 수 있게 됩니다. 

```javascript
var el = document.getElementById("outside");
el.addEventListener("click", function(evt){
 console.log(evt.target);
 console.log(evt.target.nodeName);
 debugger; //debugger를 걸면 크롬 개발자 도구에서 이 부분에서 정지한다. 그리고 source탭에 들어가서 원하는 명령어를 찍어볼 수 있다.
}, false);
```

가장 많이 쓰이는 건 event.target입니다.

event.target은 이벤트가 발생한 element를 가리킵니다. 

element도 객체이므로 안에 nodeName이나 classname과 같이 element가 가진 속성을 사용할 수 있습니다.



### 이벤트에 대한 참고 자료 

['Introduction to events'](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#Event_handler_properties)

['Event reference'](https://developer.mozilla.org/en-US/docs/Web/Events)

