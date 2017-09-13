---
layout: post
title: CSS3 - FLEXBOX
excerpt: "flexbox"
categories: [CSS]
link:
comments: true
---

flexbox를 이용하면 float랑 position이 필요없을 정도이다.

<h3>flexbox 사용시 고려해야 하는 순서</h3>

![Smithsonian Image](/img/2017-09-13-17.PNG)<br />

<h1>flexbox 사용법</h1>

<h3>1.정렬을 할 요소를 가진 부모에게 display:flex만 설정하면, flexbox 사용 준비 완료.</h3>

![Smithsonian Image](/img/2017-09-13-18.PNG)![Smithsonian Image](/img/2017-09-13-19.PNG)<br />

<h3>2.방향 결정 : 아이템을 어느 방향으로 정렬할 지를 결정하는 flex-direction: row || column;</h3>

* 자식 요소들을 가로로 배치하고 싶으면 flex-direction:row;(기본값)
* 세로로 배치하고 싶으면 flex-direction:column;

![Smithsonian Image](/img/2017-09-13-20.PNG)<br />![Smithsonian Image](/img/2017-09-13-21.PNG)![Smithsonian Image](/img/2017-09-13-22.PNG)<br />

* flex-direction: row, row-reverse(row역정렬), column, column-reverse(column역정렬);


* flex-direction에 따라 바뀌는 정렬의 기준, 두 개의 축.
flex-direction과 같은 방향의 축 : main axis (flex-direction:row일 때: 가로 / flex-direction:column일 때: 세로)
flex-direction과 수직 방향의 축 : cross axis (flex-direction:row일 때: 세로 / flex-direction:column일 때: 가로)

![Smithsonian Image](/img/2017-09-13-23.PNG)![Smithsonian Image](/img/2017-09-13-24.PNG)<br />

![Smithsonian Image](/img/2017-09-13-28.PNG)

* justify-content : center(라인마다 가운데 정렬),flex-start(라인마다 시작선을 기준으로 정렬. 만약 reverse를 했을 경우는 start의 방향도 반대로 바뀐다.),flex-end(라인마다 끝선을 기준으로 정렬. 만약 reverse를 했을 경우는 start의 방향도 반대로 바뀐다.), space-between(맨 끝 요소가 양 옆 공간에 딱 맞게 정렬되고 중간 요소들은 비례에 맞게 정렬된다.), space-around(라인 별로 각 요소의 마진 값이 똑같게 형성. 왼쪽 오른쪽의 마진 붕괴가 일어나지 않는다. 라인 별이므로 모든 요소들의 마진이 똑같아진다는 뜻이 아니다.)
* align-items(flex 컨테이너 이내에서 하나의 뭉태기로써 아이템들이 어떻게 할당될것인지를 결정한다.) : flex-start, flex-end, center, stretch, baseline, initial, inherit
* align-content(한 라인을 통째로 묶어서 움직인다. 즉, 라인 사이의 공간을 조절한다. align-items와의 차이는 아래 참고) : flex-start, flex-end, center, space-between, space-around, stretch, initial, inherit
* align-self(각각의 아이템 하나하나에 적용.) : auto(기본 값. 요소는 부모 컨테이너의 align-items 속성을 상속받는다. 만약 부모 컨테이너가 없다면 strech를 기본으로 갖는다.), stretch(요소는 컨테이너에 딱 맞게 100% 폭으로 늘어나서 위치된다.), center(컨테이너의 가운데에 위치된다.), flex-start, flex-end, baseline(컨테이너의 베이스 라인(아래 참고)에 위치된다.), inital(기본 값으로 이 요소의 속성을 고정한다.), inherit(부모 요소로부터 이 속성을 상속받는다.)

![Smithsonian Image](https://i.stack.imgur.com/bNwiG.png)

* align-items: center 와 align-content:center 비교
~~~CSS
{display:flex; flex-wrap: wrap; align-items: center || align-content:center;}
~~~

![Smithsonian Image](/img/2017-09-13-34.PNG =100px)![Smithsonian Image](/img/2017-09-13-35.PNG)<br />

* align-items: flex-start 와 align-content: flex-start 비교

~~~CSS
{display:flex; flex-wrap: wrap; align-items: flex-start; || align-content: flex-start;}
~~~

![Smithsonian Image](/img/2017-09-13-36.PNG)![Smithsonian Image](/img/2017-09-13-37.PNG)

* align-items: flex-end 와 align-content: flex-end 비교

~~~CSS
{display:flex; flex-wrap: wrap; align-items: flex-end; || align-content: flex-end;}
~~~

![Smithsonian Image](/img/2017-09-13-39.PNG)![Smithsonian Image](/img/2017-09-13-38.PNG)

* align-items: space-between 와 align-content: space-between 비교

~~~CSS
{display:flex; flex-wrap: wrap; align-items: space-between; || align-content: space-between;}
~~~

![Smithsonian Image](/img/2017-09-13-40.PNG)![Smithsonian Image](/img/2017-09-13-41.PNG)

* align-items: space-around 와 align-content: space-around 비교

~~~CSS
{display:flex; flex-wrap: wrap; align-items: space-around; || align-content: space-around;}
~~~

![Smithsonian Image](/img/2017-09-13-40.PNG)![Smithsonian Image](/img/2017-09-13-42.PNG)







<h3>3.크기를 비례하게 줄여서 한 줄만 쓸 것인가, 본래 크기를 유지한 채 다른 줄로 내려 갈 것인가.</h3>

![Smithsonian Image](/img/2017-09-13-25.PNG)<br />![Smithsonian Image](/img/2017-09-13-26.PNG)![Smithsonian Image](/img/2017-09-13-27.PNG)<br />

* flex-wrap : nowrap, wrap, wrap-reverse;

* flex-flow : flex-direction과 flex-wrap을 함께 줄여쓰는 방법이다. e.g) flex-flow: row wrap;

<h3>4.아이템들의 순서를 한 번에 바꿀 수 있다!</h3>

![Smithsonian Image](/img/2017-09-13-29.PNG)![Smithsonian Image](/img/2017-09-13-30.PNG)<br />

* 이 떄 순서 정렬시, -1 혹은 length 이상의 값을 넣으면 맨 앞이나 맨 뒤로 감
