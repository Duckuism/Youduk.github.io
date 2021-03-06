---
layout: post
title: CSS3 - BOX MODEL
excerpt: "display - block, inline, inline-block, flex, box-sizing"
categories: [CSS]
link:
comments: true
pinned: true
image:
  feature:
---

##### 참고 자료 : 멋쟁이 사자처럼 노지승님의 동영상 강의(멋쟁이 사자처럼 5기가 아니면 들을 수 없는 강의이다. 강의를 바탕으로 정리한 것이므로 문제가 될 시 자진 삭제하겠다.)

레이아웃을 잡을 때 가장 중요한 박스의 display 속성 정리

<h3>display - block</h3>

* block 속성은 기본적으로 길막을 한다! 다른 블럭들이 자기 옆에 있지 못하게 하려고 안달남
* 별도의 width 속성을 주지 않으면 자동으로 부모 컨텐츠의 width를 상속받아 width가 100%가 되어서 다른 블럭들을 밑으로 밀어버린다.

![Smithsonian Image](/img/2017-09-11-01.PNG)<br />

* width 속성 값을 설정하면 자동으로 나머지 부분을 margin으로 꽉 채워서 다른 블럭들을 밑으로 밀어버린다.

![Smithsonian Image](/img/2017-09-11-03.PNG)<br />

* 별도의 height 속성을 주지 않으면 자동으로 자식 컨텐츠들의 height의 총 합을 높이로 가진다.

![Smithsonian Image](/img/2017-09-11-02.PNG)<br />

<h3>display - inline</h3>

* inline 속성은 말 그대로 라인 안에 모든 것이 흐르는 것! 전체 라인 width가 허락하는 한 계속 옆으로 붙고, 연속적으로 붙어있는 블럭이 라인 width를 넘어서게 되면 밑으로 밀려난다.

![Smithsonian Image](/img/2017-09-11-04.PNG)
![Smithsonian Image](/img/2017-09-11-05.PNG)<br />

* 영역과 관련된 속성들이 적용되지 않는다. (라인 한 줄의 높이는 고정이므로 이 높이를 변경하는 것을 허락하지 않는 듯 하다. width,height, margin | padding -top, bottom 적용 불가. left, right는 가능.)

![Smithsonian Image](/img/2017-09-11-06.PNG)

![Smithsonian Image](/img/2017-09-11-08.PNG)<br />

<h3>display - inline-block</h3>

* inline 속성과 block 속성을 섞어 놓은 것인데, 기본적으로는 박스들이 inline 속성처럼 라인 한 줄 안에 계속 붙지만 일반 박스 모델처럼 높이에 관련된 속성을 모두 적용할 수 있다.

![Smithsonian Image](/img/2017-09-11-07.PNG)<br />

<h3>box-sizing 설정</h3>

![Smithsonian Image](/img/2017-09-11-09.PNG)
![Smithsonian Image](/img/2017-09-11-10.PNG)<br />
