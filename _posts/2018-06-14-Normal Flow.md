---
layout: post
title: Normal Flow
excerpt: "BFC, IFC, position static, position relative, float, overflow"
tags: [CodeSpitz]
categories: [CSS Rendering]
link:
comments: true
pinned: true
image:
  feature: codespitz.png
---

이 강의는 codespitz 스터디의 내용을 바탕으로 정리한 내용입니다.

<https://www.youtube.com/watch?v=_o1zsrBkZyg&t=4s>

<https://www.youtube.com/watch?v=ybNH1a14vQY&t=4s>



## Normal Flow

> Normal Flow 또한 보통 명사가 아니라 고유 명사라는 것에 주의하자. 
>
> 보통 명사 : 일반 개념을 나타내는 명사. 여러가지 사물의 공통된 특징을 나타낸다. ex) 사람, 지역, 나라 등
>
> 고유 명사 : 어느 특정한 사물에 한정하여 그 이름을 나타내는 명사 ex) 인명, 지명, 국호 등
>
> 서양에서는 고유 명사를 기존에 있는 일반 명사로 자주 정의한다.
>
> ex) domain
>
> * 일반 사람에게 domain이란? 마당
> * 개발자에게 domain이란? 인터넷의 IP를 대신하는 이름의 고유명사
>
> ex) protocol
>
> * 일반 사람에게 protocol이란? 의정서, 합의서, 계약서
> * 개발자에게 protocol이란? 네트워크 상에서 데이터를 주고 받을 때 필요한 통신 규약



CSS 2.1 visual formatting model이라는 문서가 있다.

[CSS 2.1 visual formatting model 문서 바로가기](https://www.w3.org/TR/CSS2/visuren.html)

이 문서는 어떻게 **화면에 보이는 포맷을 모델링할 것인가?**에 대한 고민들이다. 그리고 CSS 2.1에서는 Positioning Schemes & Normal Flow를 들고 있다.

Positioning Schemes 에서 **Position**이란 어떤 geometry의 left, top을 결정할 때 추상적인 위치를 결정하게 하는 일종의 시스템이다. 즉, position의 모든 속성들은 계산 공식일 뿐이다.

Position의 종류는 static / relative / absolute / fixed / inherit가 있다. 그런데 이 Position의 종류에서 <u>Normal Flow라고 부를 수 있는 속성은 static 과 relative</u> 뿐이다. 나머지는 Normal Flow가 아니다. 그렇다면 Normal Flow가 무엇일까? normal flow는 대부분의 상황들에서 웹 페이지에 요소들을 배치하는 방법 중에 하나다. (참고 : <https://www.lifewire.com/normal-flow-definition-3467023>)

Normal Flow에는 총 세 가지 속성이 있다.

1. Block Formatting Contexts (BFC)
2. Inline Formatting Contexts (IFC)
3. Relative Positioning (RP - normal flow의 일부이긴 하지만 Position 모델에서 정의하고 있으므로 현재 포스팅에서는 제외하고 뒤에 다시 다룬다.)



## BFC & IFC

그럼 하나하나의 속성을 알아보자.

BFC 에서 block이란 무엇일까?

Block은 부모의 가로 길이를 가득 채운 한 줄이다. 가로를 모두 다 차지(x 좌표는 0부터 끝까지, width:100%)하므로 다음 번 block이 나올 때 높이(y 좌표, height:???)가 어디인가만 신경쓰면 된다.

https://jsfiddle.net/Youduk_Han/bkL74p0q/

BFC는 이 Block들로 이루어진 하나의 덩어리라고 생각하면 쉽다.

![](/img/Normalflow_1.png)

BFC의 특성

* 첫 번째 block context의 height가 두 번째 block context의 y좌표 값이 된다.
* 안에 있는 블럭 요소들의 height 합이 BFC의 height가 된다.

![](/img/Normalflow_2.png)

BFC의 예시 : https://jsfiddle.net/Youduk_Han/yq8bL9p1/

IFC의 특성

* 나의 content 크기 만큼 가로를 차지한다.
  * 따라서 content가 없고, 가로 길이가 따로 지정되어 있지 않다면 IFC의 공간이 없다.
  * https://jsfiddle.net/Youduk_Han/a71ztsd8/
* 다음 번 요소의 IFC의 x 좌표 값은 첫 번째 IFC 요소의 가로길이만큼 떨어진 값이다.
* Inline 요소들의 width의 합이 부모의 width를 넘어감녀 다음 줄로 내려간다.
  * 근데 얼마나 내려가야 할까? 기준이 뭘까? 
  * 지금 Inline을 구성하고 있는 요소 중에 가장 height가 큰 값이 Line height가 되어서 Line height 만큼 y값이 내려온다.
  * base line : Inline을 구성하는 한 줄에 있는 요소 중에 제일 height가 큰 요소를 기준으로 나머지 요소들을 위, 가운데, 아래에 맞추는 세로 축 정렬 개념이 생긴다. 이것도 Inline 안에 있는 시스템인 것.

![](/img/Normalflow_3.png)

IFC의 예시 : https://jsfiddle.net/Youduk_Han/qfxbcn95/

그럼 BFC와 IFC가 함께 쓰이는 경우는 어떨까? IFC 요소가 생성되도 블럭 요소가 오면, IFC가 종료되고 격리된 상태로 블럭 요소가 들어간다.

![](/img/Normalflow_4.png)

예시 : https://jsfiddle.net/Youduk_Han/wovtcurp/

> DOM 구조와 렌더링의 구조는 무관하다! 렌더링은 시작과 끝만 탐지한다. 
>
> https://jsfiddle.net/Youduk_Han/ykwc30xs/

HTML의 span 태그는 default 속성이 inline 요소이다. 이 요소에 relative를 주면 relative position model이 적용된다. 그렇다면 relative는 어떤 모델을 갖고 있을까? relative는 static으로 일단 그리고, 상대적으로 위치를 이동시킨다. position static과 position relative가 섞여있으면 relative가 나중에 다시 그려지므로 무조건 위로 올라온다. relative끼리는 z-index로 경합을 벌인다. 

예시 : https://jsfiddle.net/Youduk_Han/vpb2rzm7/

그렇다면 relative 때문에 box의 크기 즉, width와 height가 변하는 일이 일어날까? 전혀 아니다. 오직 그림만 상대적으로 그렸을 뿐 실제 geometry 계산은 모두 static으로 한 것이다.

하지만 BFC/IFC/RP 만으로는 가로 세로로 쌓기 밖에 못하므로 그림을 다채롭게 그리기가 어렵다. 여기에 추가적인 context를 더 포함시켜서 이러한 normal flow와 상호 작용하거나 일부러 무시하는 시스템을 넣어놓은 것이 float하고 overflow이다.



## FLOAT - left / right / none / inherit

float의 속성에는 left / right / none / inherit 가 있다.

> none 같은 경우는 unset, null 등 같은 의미이지만 css 속성 별로 쓰이는 용어가 다르므로 css를 없애는 방법을 속성 별로 암기해야한다.

Float의 특성

* New BFC : float 설정 지점부터 그전까지 BFC 영역을 종결시키고 새로운 BFC 영역을 시작한다. BFC영역은 Float, Inline 영역이 차지하는 끝까지이다.
  ![](/img/Normalflow_5.png)
* Float over normal flow : float를 하면 이 이후에 선언된 normal flow에서 float 영역만 둥둥 떠있다. 그래서 이름이 float다. 
  ![](/img/Float_1.png)
  대신 여기 등장하는 모든 IFC에는 간접적인 영향을 끼친다. float가 BFC, IFC에 직접 영향을 끼치는 것은 아니지만 IFC 요소들의 가드 역할을 하게 된다. IFC 요소들이 float가 있는 곳에는 들어갈 수 없기 때문이다. BFC의 가드는 아니므로 float아래에 block 요소들은 정상적으로 그려진다. 
  ![](/img/Float_2.png)
* Line box : float는 BFC, IFC의 공식이 아니라 Line Box의 공식으로 그려진다. Line Box는 가용한 영역 중에 float가 차지하지 않은 부분으로 잡는다. 오직 float만 신경쓴다. 가로, 세로도 마찬가지. 단제 세로는 필요한 부분까지만 차지한다. 가로는 비어있으면 전체를 차지한다. 주의 할 것은 Line box는 오른쪽 왼쪽 경계면을 인식한다. 경계면 바깥의 부분은 경계가 있더라도 버리는 부분이다.
  ![](/img/Linebox_1.png)
  ![](/img/Linebox_2.png)
  ![](/img/Linebox_3.png)
  ![](/img/Linebox_4.png)
  ![](/img/Linebox_5.png)
  ![](/img/Linebox_6.png)
  ![](/img/Linebox_7.png)
  ![](/img/Linebox_8.png)
  ![](/img/Linebox_9.png)
  ![](/img/Linebox_10.png)
  ![](/img/Linebox_11.png)
  ![](/img/Linebox_12.png)



## OVERFLOW - visible / hidden / scroll / inherit / auto(default)

overflow의 속성에는 visible, hidden, scroll, inherit, auto(default)가 있다.

* visible : 보일때까지 커진다. 현재 브라우저들은 auto가 visible과 일치한다.
* hidden : 내 geometry를 넘어가는 content가 생기면 안보이게 거른다.
* scroll : 내 geometry를 넘어가는 content가 생기면 scroll bar를 만든다. 
* auto(default) : 내부에 있는 content 크기가 커지면 부모도 같이 커진다. 즉, geometry의 크기가 직접 변한다.

overflow가 hidden, scroll일 때만 flow랑 관련이 있다. 

* New BFC : overflow가  hidden 또는 scroll이라면 이 값을 갖는 요소로부터 새로운 BFC를 만든다.
* First Line Box Bound :  새로운 BFC를 만들 때 LINE BOX들의 경계면을 인식해서 영역을 잡는다. 이후에 overflow가 아닌 div가 들어오면 BFC가 확장된다. relative를 주면 이 BFC 전체가 움직이게 되는 것이다.



## OVERFLOW-X, OVERFLOW-Y - visible / hidden / scroll / clip / auto(default)

overflow를 한꺼번에 관리하지 않고 x, y축을 따로 관리하는 스펙이다.



## TEXT-OVERFLOW - clips / ellipsis