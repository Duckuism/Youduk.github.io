---
layout: post
title: ES6 const, let
excerpt: ""
categories: [JavaScriptES6]
link:
comments: true
pinned: true
image:
  feature: 

---

참고 링크

* https://github.com/sujinleeme/the-road-to-learn-react-korean/blob/master/manuscript/chapter1.md



# const, let

ES6에서 변수 선언은 const 또는 let을 사용한다. var는 거의 사용하지 않는다.

### const : 다시 할당, 선언 불가. 불변 데이터 구조(immutable data structures)

~~~javascript
//기본적으로는 불가능
const helloWorld = '리액트에 오신 여러분을 환영합니다';
helloWorld = '안녕 리액트';

//변수가 배열이나 객체일 경우는 가능. 즉, 변수가 프로퍼티나 요소를 가지고 있을 때라고 이해하는 게 올바르다고 생각 된다. 데이터 값은 변경되나 데이터 구조 자체는 변경되지 않으므로 불변 데이터 구조에 어긋나지 않는다.
const helloWorld = {
  text: '리액트에 오신 여러분을 환영합니다'
};
helloWorld.text = '안녕 리액트';
~~~



### let : 변경 가능

~~~javascript
// 가능
let helloWorld = '리액트에 오신 여러분을 환영합니다';
helloWorld = '안녕 리액트';
~~~



리액트는 불변성을 준수하므로 const가 let보다 우선이다.