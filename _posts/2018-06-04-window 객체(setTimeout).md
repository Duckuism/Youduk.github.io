---
layout: post
title: Window
excerpt: "Window 객체"
tags: [Boostcourse]
categories: [WebFE]
link:
comments: true
pinned: true
image:
  feature:
---

## window 객체

브라우저 개발을 하다 보면, window라는 객체가 있다.

window에는 많은 메서드들이 존재하며, 아래처럼 사용할 수 있는데, alert이 대표적이다.

window는 디폴트의 개념이므로 생략할 수 있다.

```javascript
window.setTimeout()
setTimeout() //window는 전역객체라서 생략 가능하다.
```

### **setTimeout 활용**

setTimeout은 낯설게 동작한다고 느낄 수 있다

인자로 함수를 받고 있으며, 즉시 실행되지 않고 나중에 실행되는 함수를 콜백함수라고 한다.

자바스크립트는 함수를 인자로 받을 수 있는 특징이 있다.

참고로 함수를 반환할 수도 있다.

```javascript
function run() {
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  //이 메시지는 즉시 실행되지 않는다. 1초 뒤에 setTimeout이 실행되면 실행된다.
    }, 1000);
}

run();
```

![](/Img/WebUI_1.png)



실행 순서를 이해하기 위해 아래와 같이 코드를 변경하고 실행해본다.

~~~ javascript
function run() {
    
    console.log("run start");
    
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  
        console.log("run .....ing");
    }, 1000);
    
    console.log("run end");
}

run();
~~~

위와 같은 코드를 실행하면 어떻게 될까?

run(); > run start() > run end() >(2초 뒤)hello codesuqad > run.....ing 순으로 실행된다.

![](/Img/WebUI_2.png)

그렇다면 아래와 같이 변경하면 어떨까?

~~~javascript
function run() {
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  
        console.log("run .....ing");
    }, 1000);    
}
console.log("run start");
run();
console.log("run end");
~~~

역시 run start() > run end() > (2초 뒤)hello codesuqad > run.....ing 순으로 실행된다.

![](/Img/WebUI_3.png)

또 다시 변경해보자

~~~javascript
function run() {
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  
        console.log("run .....ing");
    }, 1000);    
    console.log("run function end");
}
console.log("run start");
run();
console.log("run end");
~~~

![](/Img/WebUI_4.png)

이 이유는 무엇일까? 비동기 콜백 함수는 쌓였던 스택이 모두 사라지고 나서 실행되기 때문이다. 위의 코드 같은 경우는  run() 메서드는 이미 실행되고 반환이 된 상태이지만, setTimeout 안의 콜백함수는 eventQueue에 담겨있다가 스택이 다 사라지면 실행되는 것이다.

setTimeout의 특성을 잘 이해하고, 지연실행이 필요한 경우에 잘 활용하면 좋다.

### **setTimeout 실행 순서**

setTimeout의 실행은 비동기(asynchronous)로 실행되어 동기적인 다른 실행이 끝나야 실행된다.

```javascript
function run() {
    console.log("start");
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  //이 메시지는 즉시 실행되지 않는다.
    }, 1000);
    console.log("end");
}

run();
```

즉 setTimeout 안의 함수(콜백함수)는 run함수의 실행이 끝나고 나서, (정확히는 stack에 쌓여있는 함수의 실행이 끝나고 나서 실행됨) 실행된다.

디버거를 통해서 이를 스스로 직접 확인하는 것이 학습이 도움이 된다. 



어떤 분이 친절히 자세한 댓글을 달아주셨다.

k님

setTimeout 이 맨나중에 실행되는 이유는 call stack에 setTimeout이 push되고 pop되면 백그라운드에 run함수와 시간(예를들어 3초)가 보내집니다 그리고 백그라운드에서 3초를 세고 테스크큐로 넘어갑니다 이벤트 루프는 항상대기하고 있다가 call stack이 비워지면 테스크 큐에잇는 함수를 call stack으로 하나씩 밀어올립니다 

출처 : https://www.zerocho.com/category/JavaScript/post/597f34bbb428530018e8e6e2