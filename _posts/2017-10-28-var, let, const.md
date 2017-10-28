---
layout: post
title: var, let, const
excerpt: ""
categories: [Typescript]
link:
comments: true
---

### 이 강의는 타입스크립트 코리아 이웅재님의 강의를 기반으로 만들어졌습니다. 개인의 공부 및 복습 목적이므로 문제가 있으면 삭제하도록 하겠습니다.

자바스크립트는 버전에 따라서 변수를 선언하는 방식이 달리졌다.

* var(기존에 제일 많이 쓰던 방식)
* let(최근에 많이 쓰는 방식)
* const(최근에 많이 쓰는 방식)
=> 결론은 var를 안쓴다. (거의 항상 const를 씀 let은 값이 바뀔 수 있다는 여지를 주는 것이므로. const는 참조 값 자체를 리터럴 타입으로 선언되어 바꾸지 못하기 때문에 변화가 없기 때문이다.)


### var
  * ES5
  * 변수의 유효 범위 : 함수 스코프
  * 호이스팅(O) : 다짜고짜 변수를 쓰고 선언은 밑에서 하는 것.
  * 재선언 가능 : var로 할당하고 또 var로 할당해도 문제없이 돌아 감
      * 다른 언어에서는 이런 부분이 에러였다.

### let,const
  * ES6
  * 변수 유효 범위가 함수 스코프가 아니라 블록 스코프 인 것.
  * 호이스팅 불가
  * 재선언 불가.

### var 말고 let, const를 쓰자!

### 호이스팅(Hoisting)의 예

~~~javascript
console.log(hoisted_var);

var hoisted_var = '변수를 아래서 선언했는데 사용이 위에서 가능';

////////////////////////////////////////

console.log(hoisted_let);

let hoisted_let = '변수를 아래서 선언했는데 사용이 위에서 불가';
~~~

### 재할당(reclare)의 예

~~~javascript
var redeclare_var: string = '한번 선언 했는데';
var redeclare_var: string = '또 선언이 가능';
// var redeclare_var: number = 0; (X)

////////////////////////////////////////

let redeclare_let = '한번 선언 했기 때문에';
let redeclare_let = '또 선언이 불가';

/*

그렇지만 var 에서 재선언 하더라도 같은 타입이어야 함.

*/
~~~

### let과 const의 타입 추론의 차이

~~~javascript
let a: string = '에이';
let b = '비이';

const c: string = '씨이';
const d = '디이';

/*

1. a 는 명시적으로 지정된 타입인 string
2. b 는 타입추론에 의한 타입인 string
3. c 는 명시적으로 지정된 타입인 string
4. d 는 타입추론에 의한 타입인 리터럴타입 "디이" : 특수한 형태다. 리터럴 타입은 바뀔 수 없다.

*/
~~~
