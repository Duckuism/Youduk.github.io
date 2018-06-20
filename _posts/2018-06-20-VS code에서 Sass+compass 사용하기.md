---
layout: post
title: VS code에서 Sass+Compass 사용 하기!
excerpt: ""
tags: [VS CODE, Sass]
categories: [VS code]
link:
comments: true
pinned: true
image:
  feature: sass.png
---

안녕하세요! 이번에는 저번 포스팅에 이어서 VS code에서 sass와 함께 compass를 사용하는 방법을 알아보겠습니다.

## 1. Ruby 설치

먼저 compass를 설치하기 위해서는 Ruby를 설치해야합니다.

https://www.ruby-lang.org/ko/documentation/installation/

위 링크로 가셔서 미리 자신의 운영체제에 맞는 명령어를 사용해서 Ruby를 설치해주세요. 나중에 더 깊게 공부하고싶다면 미리 RVM도 설치해놓는 것이 좋습니다.(https://rvm.io/rvm/install)



## 2. Compass 설치

이제 프로젝트 폴더 내에  compass를 설치해보겠습니다.

SSH쉘로 접속합니다. (윈도우는 git bash, 맥은 터미널을 사용합니다.)

```$cd 나의 프로젝트폴더 위치``` : 먼저 cd 명령어로 내가 작업할 프로젝트 폴더 위치로 이동합니다.

![](/img/compass1.png)

```$gem update --system``` : ruby를 최신버전으로 업데이트 합니다.

![](/img/compass3.png)

```$gem install compass``` : compass를 설치합니다.

![](/img/compass4.png)

```$compass version``` : compass가 잘 설치되었는지 compass 버전을 확인해봅니다.

![](/img/compass2.png)



## 3. 프로젝트 폴더를 compass와 연결하기

이제 compass가 설치되었으니, 내 프로젝트 폴더와 compass를 연결하는 방법을 알아보겠습니다. 방법에는 두 가지가 있습니다.

1. compass watch로 내 프로젝트 폴더랑 연결하기

먼저 compass를 사용하기를 원하는 프로젝트의 폴더로 이동합니다. 저는 저번 포스팅에서 만들어두었던 vscodeProject1로 이동해볼게요. 이동하면 명령어 입력하는 부분 앞에 자신의 쉘이 위치한 폴더 트리가 보일 것입니다. 

그리고 명령어 ```$compass watch```를 입력합니다.

![](/img/compass5.png)

자, 이제 compass가 프로젝트 폴더를 감시하게 하면됩니다. 그럼 끝입니다! 이제 compass에 관련된 함수들을 모두 쓸 수 있습니다. 만약 중지하려면 control+c를 누르면 됩니다.



### 4. 내 프로젝트를 compass 프로젝트로 생성해서 연결하기

또 다른 방법으로 compass를 사용할 수 있는데요.

그 방법은 바로 compass 명령어를 통해서 프로젝트 폴더를 만드는 것입니다.

이 과정은 프로젝트 폴더 내에 compass를 설치해야하는 2번 과정을 건너뛸 수 있게 해줍니다.

대신 이 과정은 프로젝트 폴더 내에 compass가 설치되어 있는 것이 아니라, global로 compass가 설치되어 있어야합니다.(root 폴더에서 ```$ gem install compass``` 명령어 수행)

이번에는 compass 명령어로 프로젝트를 만들어야 하므로 먼저 프로젝트 폴더가 생성되길 원하는 위치로 이동합니다. 

![](/img/compass6.png)

```$compass create vscodeProject2``` : 프로젝트 폴더가 생성되길 원하는 위치에서 compass폴더를 생성합니다.

![](/img/compass7.png)

```$cd vscodeProject2``` : 그리고 생성된 폴더 안으로 이동합니다.

![](/img/compass8.png)

```$compass watch``` : 이제  compass watch를 실행합니다.

![](/img/compass9.png)

위의 코드 세줄은 scss가 변경되는 때마다 자동적으로 css로 컴파일 하겠다는 것을 의미합니다.



## 5. compass 사용하기

이제 본격적으로 compass를 사용해보겠습니다.

가장 먼저 해야할 것은 scss파일에서 @import 구문을 통해 compass를 사용하겠다고 명시하는 것입니다.

compass는 모듈로 나눠져 있으므로 각각의 모듈들을 사용하기 위해서는 먼저 원하는 모듈을 scss파일로 import하여 가져온 후 사용해야합니다. compass의 모듈 종류를 한 번 볼까요?

* Browser Support : ```@import "compass/support"```
  http://compass-style.org/reference/compass/support/
* CSS3 : ```@import "compass/css3"```
  http://compass-style.org/reference/compass/css3/
* Helpers : Helper는 따로 import가 필요하지 않습니다. 기존에 Sass가 제공하는 함수들을 더 효과적으로 사용할 수 있게해줍니다.
  http://compass-style.org/reference/compass/helpers/
* Layout : ```@import "compass/layout"```
  http://compass-style.org/reference/compass/layout/
* Reset : ```@import "compass/reset"```
  http://compass-style.org/reference/compass/reset/
* Typography : ```@import "compass/typography"```
  http://compass-style.org/reference/compass/typography/
* Utilities : ```@import "compass/utilities"```
  http://compass-style.org/reference/compass/utilities/

예시를 위해 scss 파일을 열고 맨 위에 다음 코드를 추가해보겠습니다. compass의 css3 모듈을 사용하겠다는 뜻입니다.

```@import "compass/css3"```

그럼 일반 css를 사용할 때랑 compass의 css모듈을 사용할 때랑 차이를 볼까요?

만약 일반 css를 사용할 때 3개의 column에 20px의 gutter를 준다면 코드는 다음과 같습니다.

```scss
div
{
        -webkit-column-count:3;
        -moz-column-count:3;
        column-count:3;
        -webkit-column-gap:20px;
        -moz-column-gap:20px;
        column-gap:20px;
}
```

하지만 compass/css3 모듈을 통해 사용한다면 코드가 다음과 같습니다

```scss
div
{
        @include column-count(3);
        @include column-gap(20px);
}
```

우리가 웹표준을 지키기 위해서 사용하던 vendor prefix가 다 사라진 걸 볼 수 있죠? 엄청나네요!



만약 background-image에 gradient를 지정해야할 때는 어떨까요?

먼저 일반 css를 사용할 때입니다.

```scss
.gradient
{
        background-image: -webkit-gradient(linear, 50% 0%, 50% 100%, color-stop(0%, #ffffff), color-stop(100%, #000000));
        background-image: -webkit-linear-gradient(#ffffff, #000000);
        background-image: -moz-linear-gradient(#ffffff, #000000);
        background-image: -o-linear-gradient(#ffffff, #000000);
        background-image: linear-gradient(#ffffff, #000000);
}
```

그리고 compass/css3 모듈을 사용할 때입니다.

```scss
.gradient
{
        @include background-image(linear-gradient(#fff, #000));
}
```

엄청나죠..?

이렇게 유용한 compass, 꼭 sass랑 같이 쓰세요!

다음 포스팅에서 뵙겠습니다~!!







참고: 

* http://compass-style.org/install/
* http://compass-style.org/help/
* http://compass-style.org/reference/compass/
* http://thesassway.com/beginner/getting-started-with-sass-and-compass
* https://stackoverflow.com/questions/18375691/does-import-compass-includes-the-whole-framework
* https://www.webdesignerdepot.com/2013/11/how-to-write-simple-elegant-css-with-compass-sass/