---
layout: post
title: 4. Type assertions, Type alias
excerpt: ""
categories: [Typescript]
link:
comments: true
---

### 이 강의는 타입스크립트 코리아 이웅재님의 강의를 기반으로 만들어졌습니다. 개인의 공부 및 복습 목적이므로 문제가 있으면 삭제하도록 하겠습니다.

### Type assertions

* 형변환과 다르다. (형변환은 실제 데이터 구조를 바꾼다.)
* '타입이 이것이다'라고 컴파일러에게 알려주는 것을 의미. 즉, 일시적으로 컴파일러가 인식하는 타입을 강제로 지정하는 것.(컴파일러가 속는다. 이것은 런타임에서 에러가 날 수 있다는 뜻과 같다.)
    * 따라서 type assersions에 대해서 작성자가 100% 신뢰하고 사용하는 것이 중요하다.
* 문법적으로는 두 가지 방법이 있다.
    * 변수 as 강제할 타입
    * <강제할타입>변수 (문서에는 이 표현 방식은 JSX에서 헷갈릴 우려가 있으므로 피하라고 권함. 따라서 위의 방법으로 사용하길 추천)

~~~Javascript

let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
let strLength: number = (someValue as string).length;

/*

1. 주로 넓은 타입에서 좁은 타입으로 강제하는 경우가 많다.
2. jsx 에서는 as 를 쓴다.

*/

~~~

### Type ALIAS

* 타입 별칭(별명) => 타입을 변수에 넣어서 그 변수를 쓴다는 느낌.
* 인터페이스랑 유사
* 주로 쓰는 경우
    * primitive 타입을 다른 이름으로 부를 때,
    * union type, tuple을 여러번 쓸 때 계속 쓰기 귀찮으니까 이 변수를 이것이라고 부른다는 형식으로 따로 빼서 반복 사용,
* 기타 직접 작성해야하는 타입을 다른 이름으로 지정할 수 있다.
* 만들어진 타입의 참조로 사용하는 것이지 타입을 만드는 것은 아니다.

##### Aliasing Primitive

~~~javascript
type MyStringType = string;

const str = 'world';

let myStr: MyStringType = 'hello';
myStr = str;

/*

별 의미가 없다..

*/
~~~

##### Union Type

유니온 타입 : a도 될 수 있고, b도 될 수 있고, c도 될 수 있다.
(any랑 유사하지만 좀 더 구체적이다. any는 모든 것이 되지만 union type은 가능성이 있는 것들을 제한하므로)

~~~javascript
1) type alias를 쓰기 전

let a: any;
let b: string | number;

b = '스트링';
b = 0;

function test(arg: string | number): string | number {
  return arg;
}
~~~

~~~javascript
2) type alias를 쓴 후
let a: any;

type StringOrNumber = string | number;

let b: StringOrNumber;

b = '스트링';
b = 0;

function test(arg: StringOrNumber): StringOrNumber {
  return arg;
}
~~~

##### Aliasing Union Type

~~~javascript
let person: string | number = 0;
person = 'Mark';

type StringOrNumber = string | number;

let another: StringOrNumber = 0;
another = 'Anna';

/*

1. 유니온 타입은 A 도 가능하고 B 도 가능한 타입
2. 길게 쓰는걸 짧게

*/
~~~

### Aliasing Tuple

~~~javascript
let person: [string, number] = ['Mark', 35];

type PersonTuple = [string, number];

let another: PersonTuple = ['Anna', 24];

/*

1. 튜플 타입에 별칭을 줘서 여러군데서 사용할 수 있게 한다.

*/
~~~

### keyof 키워드 사용 관련 동영상
<https://www.youtube.com/playlist?list=PLV6pYUAZ-ZoE8uRXG51003heNA0EATIxN>

### interface와의 차이점

#### 차이점 1

~~~javascript
type Alias = { num: number }

interface Interface {
    num: number;
}

declare function aliased(arg: Alias): Alias;
declare function interfaced(arg: Interface): Interface;

/*

1. type alias 는 object literal type 로
2. interface 는 interface 로

오류가 났을 때 컴파일러가 알려주는 형식이 다르다. Interface는 타입 Interface로 알려주지만, Alias는 { num : number}라고 알려준다.

*/
~~~

#### 차이점 2

~~~javascript
type PersonAlias = {
    name: string;
    age: number;
};

interface IPerson extends PersonAlias {

}

let ip: IPerson = {
    name: 'Mark',
    age: 35
};

class PersonImpl implements PersonAlias {
    name: string;
    age: number;

    hello() {
        console.log('안녕하세요');
    }
}

let pi: PersonImpl = new PersonImpl();
pi.hello();

class PersonChild extends PersonAlias {
  //클래스가 인터페이스를 상속받아서 구현하는 것처럼 클래스가 typeAlias를 상속받는 것은 안된다. 즉 typeAlias가 다른 것을 상속 받을 수는 있지만, 다른 것에 상속할 수는 없다. typeAlias는 인터페이스와 유사한 것이지 인터페이스는 아니기 때문
}


/*

1. 당연한건 type alias 끼리는 extends, implements 불가
2. interface extends type alias 가능
3. class implements type alias 가능
4. class extends type alias 블가 (interface 도 마찬가지)
5. 마치 interface 처럼 동작한다.

*/


/*
type alias로 지정한 것들끼리 상속과 구현이 불가능하다. 어찌보면 각자 다른 리터럴 타입이므로 타입끼리 상속과 구현을 한다는 것인데, 말이 되지 않기도 함.

그러나 인터페이스처럼 클래스가 type alias를 상속받아서 구현하고, 인터페이스가 type alias를 상속하는 등의 형식 즉, 인터페이스 수즌의 형식은 가능하다. 그러나 만약 무언가 에러가 나면 인터페이스는 어떤 인터페이스에서 에러가 났다고 알려주겠지만, type alias는 참조하는 리터럴 타입을 알려주므로 어디서 에러가 났는지 알아보기가 힘들다. 따라서 같은 코드라면 인터페이스를 쓰지, 굳이 type alias를 써서 알아보기 어렵게 할 필요가 없다.
*/
~~~
