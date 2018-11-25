---
layout: post
title: Web Annimation
excerpt: "setTimeout, requestAnimationFrame, CSS3 transition"
tags: [Boostcourse]
categories: [WebFE]
link:
comments: true
pinned: true
image:
  feature: Boostcourse.png
---



## **1. 애니메이션**

애니메이션은 반복적인 움직임의 처리입니다.

웹 UI 애니메이션은 자바스크립트로 다양하게 제어할 수 있지만, 규칙적이고 비교적 단순한 방식으로 동작하는 방식은 CSS3의 transition과 transform속성을 사용해서 대부분 구현 가능합니다.

그뿐만 아니라 자바스크립트보다 더 빠른 성능을 보장한다고 합니다.

이런 애니메이션 성능 비교가 된 글을 찾아보고 비교해봅니다.

특히 모바일 웹에서는 CSS를 사용한 방법이 훨씬 더 빠릅니다.

## **2. FPS**

FPS (frame per second)는 1초당 화면에 표현할 수 있는 정지화면(frame) 수입니다.

매끄러운 애니메이션은 보통 60fps 입니다.

따라서 16.666밀리세컨드 간격으로 frame 생성이 필요한 셈이죠. (1000ms / 60fps = 16.6666ms)

앞서 말한 것처럼, 애니메이션은 CSS의 transition속성으로 CSS 속성을 변경하거나, JavaScript로 CSS 속성을 변경할 수 있습니다.

결국 이렇게 정의할 수 있습니다.

- 간단하고 규칙적인 거 → CSS로 변경
- 세밀한 조작이 필요한 거 → JavaScript로 변경

성능만 봐서는 대체로 CSS로 변경하는 것이 빠릅니다.

하지만 성능 비교를 통해서 가장 빠른 방법을 찾는 과정이 필요하기도 합니다.

## **3. JavaScript 애니메이션**

자바스크립트로 애니메이션을 구현하려면, 규칙적인 처리를 하도록 구현하면 됩니다.

다음과 같은 방법이 있습니다.

- setInterval
- setTimeout
- requestAnimationframe
- Animations API

#### **3.1 setInterval()**

주어진 시간에 따라서 함수 실행이 가능합니다.

```javascript
const interval = window.setInterval(()=> {
  console.log('현재시각은', new Date());
},1000/60);

window.clearInterval(interval);
```

하지만 지연문제가 발생할 수 있습니다.

아래 그림을 보면 제때 일어나야 할 이벤트 콜백이 중간에 일어나는 다른 이벤트들로 인하여 지연되거나 없어지는 것을 볼 수 있습니다.

따라서 setInterval을 사용한다고 해서 정해진 시간에 함수가 실행된다고 보장할 수 없습니다. 이러한 이유로 일반적으로 setInterval을 사용하는 애니메이션 구현은 잘 하지 않습니다.

[![img](https://cphinf.pstatic.net/mooc/20180205_116/1517816517181oVblH_PNG/3-4-1_setInterval.png?type=w760)](https://www.edwith.org/boostcourse-web/lecture/16752/#)

- **setInterval**


#### **3.2 setTimeout**

```javascript
//arrow 함수를 사용했어요.
  setTimeout(() => {
    console.log('현재시각은', new Date());
  },500);
```

애니메이션을 구현하려면 재귀호출을 해서 구현할 수 있습니다.

```javascript
let count = 0;
function animate() {   
  setTimeout(() => {
    if(count >= 20) return;
    console.log('현재시각은', new Date());
    count++;
    animate();
  },500);
}
animate();
```

setTimeout도 엄밀하게는 어떤 이유로 인해 제때에 원하는 콜백함수가 실행되지 않을 수는 있습니다. 결국 setInterval과 같은 문제가 발생할 수도 있긴합니다.  하지만 그럼에도 setTimeout은 매 순간 timeout을 조절할 수 있는 코드구현으로 컨트롤 가능한 부분이 있다는 점이 setInterval과 큰 차이라고 할 수 있습니다.

------

**생각해보기**

1. 동일한 요구사항을 만들고, setInterval로 애니메이션을 했을 경우와 setTimeout으로 애니메이션을 구현했을 경우를 비교해보면서 실험해보면 좋습니다. 

------

**참고 자료**

[![img](https://cphinf.pstatic.net/mooc/20180205_40/1517817270088GIB7P_PNG/R0hp0pf56OIG8ibDbomh.png?type=mfullfill_199_148)](https://javascript.info/settimeout-setinterval)

- **[참고링크] Scheduling 참고 글과 예제**<https://javascript.info/settimeout-setinterval>



#### **3.3 requestAnimationFrame**

setTimeout은 animation을 위한 최적화된 기능이라 보기는 어렵습니다.

animation주기를 16.6 미만으로 하는 경우 불필요한 frame 생성이 되는 등의 문제가 생깁니다.

그 대안으로 생긴 것이 바로 requestAnimationFrame입니다.

아래 예제를 살펴보시죠.

먼저 아래처럼 requestAnimationFrame을 한번 실행시켜줘야 합니다.

그 이후에 특정 조건이 될 때까지(함수의 탈출 조건) 계속 함수를 연속적으로 호출하는 것이죠.

이렇게 requestAnimationFrame함수를 통해서 원하는 함수를 인자로 넣어주면, 브라우저는 인자로 받은 그 비동기 함수가 실행될 가장 적절한 타이밍에 실행시켜줍니다.

우리는 어느 정도 브라우저를 믿고 이 함수를 전달해주는 것입니다. 

```javascript
var count = 0;
var el=document.querySelector(".outside");
el.style.left = "0px";

function run() {
   if(count > 70) return;
   count = count + 1;
   el.style.left =  parseInt(el.style.left) + count + "px";
   requestAnimationFrame(run);
}

requestAnimationFrame(run);
```

예제에서는 연속적으로 requestAnimationFrame를 통해서 run함수를 호출하면서 left 값을 증가시켜주고 있습니다. 

(횟수로 70회까지 테스트하는 코드입니다.)

canvas, svg를 사용하면서 그래픽 작업을 하게 될 때 복잡한 애니메이션을 다룰 필요가 생길 수 있습니다.

자바스크립트로 복잡한 애니메이션처리를 처리해야 할 때 requestAnimationFrame은 꽤 유용하게 쓰일 수 있습니다.

count를 통해서 일정 횟수로 애니메이션이 동작하도록 했지만, 시간값을 이용한다면, 일정시간안에서만 애니메이션이 

발생하도록 할 수도 있을 것입니다. 아래 참고링크MDN사이트의 예제를 살펴보세요!

------

**생각해보기**

1. requestAnimationFrame을 통한 함수호출을 여러 번 해보면 어떨까요? 예를 들어 requestAnimationFrame(run), 그리고 requestAnimationFrame(run2) 이런 식으로 1개 이상의 애니메이션 동작을 한 페이지에서 구현하면 어떤 결과가 나올지 확인해보세요. 많을수록 테스트가 더 의미 있을 겁니다. 브라우저마다 결과가 다를 수 있지만, 아마도 브라우저는 처리해야 할 애니메이션 함수들을 열심히 호출하면서 최대한 자연스러운 애니메이션 결과를 보여주려고 할 겁니다. 이런 상태에서 더욱더 requestAnimationFrame이 의미가 있다고 봐야겠습니다.

------

**참고 자료**

[![img](https://cphinf.pstatic.net/mooc/20180205_224/1517819728073Mmhvp_PNG/MLFR6chxvyyt9TQE7aF9.png?type=mfullfill_199_148)](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)

- **[참고링크] window.requestAnimationFrame()**<https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame>


## **CSS 기법으로 애니메이션 구현**

transition 을 이용한 방법입니다.  모든 CSS속성을 1초 동안 변화하게 한다. 애니메이션 속성(예를 들어 transform)만 변화하게한다고 볼 수는 없고, 변할 수 있는 모든 속성이 대상이 될 수 있다. left나 top같은 고정 값을 변화 시키는 것도 1초 동안 천천히 변화하게 되는 것. transform: scale()과 left를 같이 변화하게 하면 오른쪽으로 움직이면서 커진다 굉장히 재밌다ㅋㅋㅋㅋ 만약 특정 애니메이션 속성만 제어한다고 하면 ```transition: scale 2s;``` 이런 형식으로 하거나, ```transition: transform 2s;```  처럼 transform에만 적용되게 할 수 있다.

이 방법이 JavaScript로 구현하는 것보다 더 빠르다고 알려져 있다.  

특히 모바일 웹에서는 transform을 사용한 element의 조작을 많이 구현합니다.

[링크 바로가기](https://robots.thoughtbot.com/transitions-and-transforms)

**더 빠른 css3 애니메이션 관련 속성들**

GPU가속을 이용하는 속성을 사용하면 애니메이션 처리가 빠릅니다.

- transform : translateXX();
- transform : scale();
- transform : rotate();
- opacity

아래 링크를 참고해보세요.

[링크 바로가기](https://d2.naver.com/helloworld/2061385)

------

**생각해보기**

1. 특정 엘리먼트를 만들고, 그 엘리먼트에 transition 속성을 주고, hover했을 때 좌측 상단에서, 우측 하단으로 움직이는 animation을 만들어보세요.
2. vendor prefix가 무엇이고, 왜 필요한지 알아봅니다.

------

**참고 자료**

- **[참고링크] 하드웨어 가속에 대한 이해와 적용**<https://d2.naver.com/helloworld/2061385>


- **[참고링크] CSS Transitions and Transforms for Beginners**<https://robots.thoughtbot.com/transitions-and-transforms>


[![img](https://cphinf.pstatic.net/mooc/20180205_3/1517820854258CNq5i_PNG/hXCxK3IwoBuOMVPxTxCm.png?type=mfullfill_199_148)](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)

- **[참고링크] window.requestAnimationFrame()**<https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame>