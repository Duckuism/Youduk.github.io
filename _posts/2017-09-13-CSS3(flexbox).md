---
layout: post
title: CSS3 - FLEXBOX
excerpt: "FLEXBOX"
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

![Smithsonian Image](/img/2017-09-13-20.PNG)![Smithsonian Image](/img/2017-09-13-21.PNG)![Smithsonian Image](/img/2017-09-13-22.PNG)<br />

* flex-direction에 따라 바뀌는 정렬의 기준, 두 개의 축.
flex-direction과 같은 방향의 축 : main axis
flex-direction과 수직 방향의 축 : cross axis

![Smithsonian Image](/img/2017-09-13-23.PNG)![Smithsonian Image](/img/2017-09-13-24.PNG)<br />

![Smithsonian Image](/img/2017-09-13-28.PNG)

* justify-content : center(라인마다 가운데 정렬),flex-start(라인마다 시작선을 기준으로 정렬),flex-end(라인마다 끝선을 기준으로 정렬), space-between(맨 끝 요소가 양 옆 공간에 딱 맞게 정렬되고 중간 요소들은 비례에 맞게 정렬된다.), space-around(라인 별로 각 요소의 마진 값이 똑같게 형성. 왼쪽 오른쪽의 마진 붕괴가 일어나지 않는다. 라인 별이므로 모든 요소들의 마진이 똑같아진다는 뜻이 아니다.)
* align-items(아이템들을 통째로 움직인다.) : flex-start, flex-end, center, space-between
* align-content(아이템 하나하나 움직인다.) : flex-start, flex-end, center, space-between

<h3>3.크기를 비례하게 줄여서 한 줄만 쓸 것인가, 본래 크기를 유지한 채 다른 줄로 내려 갈 것인가.</h3>

![Smithsonian Image](/img/2017-09-13-25.PNG)![Smithsonian Image](/img/2017-09-13-26.PNG)![Smithsonian Image](/img/2017-09-13-27.PNG)<br />

<h3>4.아이템들의 순서를 한 번에 바꿀 수 있다!</h3>

![Smithsonian Image](/img/2017-09-13-29.PNG)![Smithsonian Image](/img/2017-09-13-30.PNG)<br />
