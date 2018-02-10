---
layout: post
title: ES6 arrow function
excerpt: "화살표 함수"
categories: [JavaScriptES6]
link:
comments: true
pinned: true
image:
  feature: 

---

참고 자료

* https://github.com/sujinleeme/the-road-to-learn-react-korean/blob/master/manuscript/chapter1.md
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions

~~~javascript
//기존의 함수 표현식
function () { ... }//this : 자기 자신을 this객체로 생성하여 자기 자신을 지칭


// 화살표 함수 표현식
() => { ... }//this: 자기 자신을 this객체로 생성하지 않고 자신을 감싸고 있는 컨텍스트를 지칭

this의 차이점이 있으므로 유심히 봐 둘 것.
ES 3,5에서는 사용되지 않을 변수에 this의 값을 할당하게 되어 문제가 되었었다.


// 가능
item => { ... }

// 가능(단일 매개변수 일 때 생략 가능)
(item) => { ... }

// 불가능(복수 매개변수 일 때 생략 불가)
item, key => { ... }

// 가능
(item, key) => { ... }

// 블록 본문 중괄호 생략 가능
// 중괄호가 생략된 본문을 '간결한 본문'이라고 지칭
// 간결한 본문에는 반환(return)이 포함되어 기존에 존재하면 return문 삭제 가능
(item, key) => ...
~~~

