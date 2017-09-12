---
layout: post
title: CSS3 - position
excerpt: "position - static, relative, absolute, fixed"
categories: [CSS]
link:
comments: true
---

float랑 position을 언제 써야할까?

float는 부모의 영역 속에 제한되는 느낌이고, position은 화면 안에서 자유자재로 움직일 수 있다. 내가 해당 요소를 써야하는 기능과 이유를 잘 생각해보고 맞는 것을 골라 쓰면 된다.

<h1>POSITION</h1>

position에서 고려해야 될 것 : 종류(내가 어떤 종류의 position을 쓰는지, 종류에 따라 작용하는 방법이 다르므로) && 기준점(기준점이 position에 따라 달라지므로)

<h1>POSITION - static</h1>

<h3>기본 position은 항상 static!(top,bottom,left,rigth 속성이 안 먹힌다.)</h3>

<h1>POSITION - relative</h1>

float와 같이 붕 뜨기는 하지만 자신이 있던 곳의 기준점을 잊지 않고 이 기준점을 기준으로 움직인다. 그리고 다른 요소들도 이 relative를 인식할 수 있기 때문에 당겨지거나 하지 않는다.

![Smithsonian Image](/img/2017-09-13-01.PNG)<br />

![Smithsonian Image](/img/2017-09-13-02.PNG)<br />

![Smithsonian Image](/img/2017-09-13-03.PNG)<br />

![Smithsonian Image](/img/2017-09-13-04.PNG)<br />


<h1>POSITION - absolute</h1>

***absolute는 float와 유사하지만 inline요소들이 인식할 수 없다는 점이 가장 큰 차이이다. 또한, overflow:hidden / cleaf:both 같이 다시 인식할 수 있는 방법이 없다. 그래서 float가 집 가간 자식이라면 absolute는 버린 자식이라고 표현하는 것.*** float 속성을 적용했을 때 처럼 absolute를 적용하는 순간, display 값은 block으로 바뀌는 데, block은 길막을 하지 않는 block이라서 contents만큼의 width를 갖는 블록이다. width를 설정해 주지 않았을 때 부모의 width만큼 자동으로 차지하거나, width를 설정해 주었을 때 남는 부분이 모두 margin으로 변하는 등의 현상이 일어나지 않는다.

![Smithsonian Image](/img/2017-09-13-05.PNG)<br />

기준점이 부모 요소에 한정되는 float속성과 달리, absolute는 조건이 맞다면(position이 static이 아닌 relative, absolute, fixed 라면) 조상 요소들 중에 하나로 기준 점을 새로 정할 수 있다. 이 떄 조상 요소의 postion은 보통 absolute가 아닌 relative로 많이 주는데, absolute로 조상 요소의 기준을 잡게 될 경우 이 요소 또한 자신의 조상 중에 조건이 맞는 조상을 기준으로 삼게 되므로 기준점을 생각하기가 복잡해지기 때문이다.

![Smithsonian Image](/img/2017-09-13-06.PNG)<br />

![Smithsonian Image](/img/2017-09-13-08.PNG)<br />

![Smithsonian Image](/img/2017-09-13-09.PNG)<br />

![Smithsonian Image](/img/2017-09-13-10.PNG)<br />

<h1>POSITION - fixed</h1>

기본 속성은 absolute랑 똑같다. absolute를 적용했을 때처럼 길막할 수 없는 block이 되고, inline요소들이 인식할 수 없고, 다시 인식하게 할 수 있는 방법이 없다는 것은 같다. ***한 가지 차이점은 우리가 기준점을 생각할 필요없이 무조건 viewport(웹사이트가 보여지는 창의 전체 크기)를 기준으로 위치한다는 것이다.***

![Smithsonian Image](/img/2017-09-13-11.PNG)<br />

![Smithsonian Image](/img/2017-09-13-12.PNG)<br />


<h1>POSITION - offset</h1>

position을 설정하는 것은 내가 어떤 기준으로 움직일 것인지를 선언하는 것일 뿐, 실제로 움직이는 것은 아니다. 따라서 position을 설정했다고 해서 해당 position 속성의 기준점으로 요소가 움직이지 않는 것이다. 이 요소를 움직이려면 top, bottom, left, right 값으로 움직여야 한다.

이 기준점 위치를 움직이는 방법이 바로 offset이다. offset은 X축(top, bottom)에 하나, Y축(left, right)에 각각 하나씩만 가져야 한다.

![Smithsonian Image](/img/2017-09-13-13.PNG)<br />

![Smithsonian Image](/img/2017-09-13-14.PNG)<br />

![Smithsonian Image](/img/2017-09-13-15.PNG)<br />

![Smithsonian Image](/img/2017-09-13-16.PNG)<br />
