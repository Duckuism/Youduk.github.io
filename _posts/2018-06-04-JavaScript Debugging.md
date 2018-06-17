---
layout: post
title: Javascript debugging
excerpt: ""
tags: [Boostcourse]
categories: [WebFE]
link:
comments: true
pinned: true
image:
  feature:
---

## JavaScript Debugging

debugging : 버그를 잡는 행위.

자바스크립트는 브라우저 런타임단계에서 실행되기 때문에 브라우저에서 디버깅을 많이 한다.

ToDoMVC.com 

소스 탭에서 원하는 소스 파일을 클릭하고 break point를 잡으면 실행이 되다가 해당 부분에서 멈춘다. ESC를 누르면 console창이 나타나는데, 여기서 코드를 입력하면서 여러가지를 확인할 수 있다. 또한 오른쪽에 debugging tap의 call stack에서 쌓인 스택들을 볼 수 있다.

원하는 함수의 안으로 들어가고 싶으면 step into를 누르면 된다. dubugging tap의 Local tap은 현재 함수에서의 지역변수 값들을 나타낸다.

console.log() 나 alert() 대신에 디버깅을 하는 습관을 들이자!!



### **디버깅 컨트롤**

- Pause, Continue : 첫 번째 버튼은 평소에는 Pause 버튼 상태인데 브렉포인트가 잡힌 상태에선 Continue 버튼이 된다. 다른 브레이크포인트가 잡힐 때까지 코드를 진행한다.
- Step over next function call : 스텝 오버는 코드 라인을 한 스탭 진행하는데 현재 실행 라인에 함수 실행 코드가 있다면 함수는 실행하는데 이때 함수 안의 코드로는 진입하지 않는다. 즉 라인의 함수를 실행만 하게 된다.
- Step into next function call : 스텝 인투는 스텝 오버와 다르게 현재 실행 라인의 코드에 함수가 있다면 함수 안의 첫 번째 코드로 진입해 들어가 다시 하나씩 라인별로 코드를 실행할 수 있다.
- Step out of current function : 스텝 인투로 들어온 함수를 끝까지 실행하고 밖으로 빠져나와 해당 함수를 실행한 함수로 돌아간다.
- Active/Deactive breakpoint : 브레이크포인트를 끄거나 켤 수 있다.
- Pause on exception : 자바스크립트 예외가 발생하면 해당 위치에 브레이크포인트를 잡아준다.

------

### **생각해보기**

1. 본인이 개발 중 인코드의 디버깅을 지금 배운 내용으로 해본다. 디버깅을 통한 개발방법도 일종의 습관이다.
2. 구글 검색창에 '크롬 개발자 도구 자바스크립트 디버깅'을 입력해서 학습해보자.