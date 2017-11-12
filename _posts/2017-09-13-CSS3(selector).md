---
layout: post
title: CSS3 - SELECTORS
excerpt: "selectors"
categories: [CSS]
link:
comments: true
pinned: true
image:
  feature: css.jpg
---

###### 참고 : https://www.w3schools.com/cssref/css_selectors.asp

<h3>CSS SELECTORS</h3>

CSS에서 셀렉터란 내가 원하는 스타일을 적용하기위한 요소를 선택하는데 사용되는 패턴이다.
맨 오른쪽의 CSS컬럼은 해당 셀렉터가 적용된 CSS버전을 나타낸다.

| <center>셀렉터</center> | <center>사용 예</center> |           <center>설명</center>            | <center>CSS</center> |
| :------------------: | :-------------------: | :--------------------------------------: | :------------------: |
|                      |                       |                                          |                      |
|        .class        |        .intro         |     클래스 속성명이 intro인 속성을 가진 모든 요소 선택      |          1           |
|         #id          |      #firstname       |   아이디 속성명이 firstname인 속성을 가진 모든 요소 선택    |          1           |
|          *           |           *           |                 모든 요소 선택                 |          2           |
|       element        |           p           |         <p>태그 요소들을 가진 모든 요소들 선택          |          1           |
|   element,element    |         div,p         |         모든 \<div>태그와 \<p>태그들 선택          |          1           |
|   element element    |         div p         |        \<div>태그 안에 \<p>태그 요소들을 선택        |          1           |
|   element>element    |         div>p         |       부모 요소가 \<div>인 \<p>태그들 모두 선택       |          2           |
|   element+element    |         div+p         |    <div>요소들 바로 다음에 위치한 모든 \<p>태그들 선택     |          2           |
|  element1~element2   |        p ~ ul         |       \<p> 요소 앞에있는 모든 \<ul> 요소를 선택       |          3           |
|     [attribtute]     |       [target]        |        target 속성과 같이 있는 모든 요소들 선택        |          2           |
|  [attribute=value]   |    [target=_blank]    |       타겟 속성 값이 "_blank"인 모든 요소들 선택       |          2           |
|  [attribute~=value]  |    [title~=flower]    |  타이틀 속성 값에 단어 "flower"를 포함하는 모든 요소들 선택   |          2           |
| [attribute\|=value]  |      [lang\|=en]      |     lang 속성 값이 "en"으로 시작하는 모든 요소들 선택     |          2           |
|  [attribute^=value]  |   a[href^="https"]    | "https"로 시작하는 href 속성 값을 가진 모든 \<a>태그 요소들 모두 선택 |          3           |
|  [attribute$=value]  |    a[href$=".pdf"]    | ".pdf"로 끝나는 href 속성 값을 가진 \<a>태그 요소들 모두 선택 |          3           |
|  [attribute*=value]  | a[href*="w3schools"]  |  "w3schools"를 문자열로 가진 모든 \<a>태그 요소들 선택   |          3           |
|       :active        |       a:active        |               active 링크 선택               |          1           |
|       ::after        |       p::after        |         각각의 \<p>태그 내용 뒤에 무언가를 삽입         |          2           |
|       ::before       |       p::before       |         각각의 \<p>태그 내용 전에 무언가를 삽입         |          2           |
|       :checked       |     input:checked     |           모든 체크된 \<input>태그 선택           |          3           |
|      :disabled       |    input:disabled     |          모든 사용불가된 \<input>태그 선택          |          3           |
|        :empty        |        p:empty        | (텍스트 노드를 포함한) 어떤 자손도 가지지 않은 \<p>태그 요소 선택 |          3           |
|       :enabled       |     input:enabled     |        사용할 수 있는 모든 \<input>태그 선택         |          3           |
|     :first-child     |     p:first-child     |       부모 요소의 첫번째 자손인 모든 \<p>태그 선택        |          2           |
|    ::first-letter    |    p::first-letter    |           모든 \<p>태그의 첫번째 문자 선택           |          1           |
|     ::first-line     |     p::first-line     |           모든 \<p>태그의 첫번째 줄 선택            |          1           |
|    :first-of-type    |    p:first-of-type    | 부모 요소를 가진 첫번째 태그의 타입이 \<p>인 \<p>태그 모두 선택(게시글 맨 아래 first와의 차이점 참고) |          3           |
|        :focus        |      input:focus      |     focus 속성을 가진 \<input>태그 요소 모두 선택     |          2           |
|        :hover        |        a:hover        |            마우스 오버된 링크를 선택한다.             |          1           |
|      :in-range       |    input:in-range     |   특정한 범위 내에 하나의 값을 가진 모든 \<input>태그 선택   |          3           |
|       :invalid       |     input:invalid     |      유요하지 않은 값을 가진 모든 \<input>태그 선택      |          3           |
|   :lang(language)    |      p:lang(it)       | "it(Italian)"과 같은 lang속성 값을 가진 모든 \<p>태그 선택 |          2           |
|     :last-child      |     p:last-child      |       부모 요소의 마지막 자손인 모든 \<p>태그 선택        |          3           |
|    :last-of-type     |    p:last-of-type     |        부모의 마지막 \<p>타입인 \<p>요소 선택         |          3           |
|        :link         |        a:link         |             방문하지 않은 모든 링크 선택             |          1           |
|    :not(selector)    |        :not(p)        |         \<p>태그가 아닌 나머지 모든 요소 선택          |          3           |
|    :nth-child(n)     |    p:nth-child(2)     |         부모의 두번째 자손인 모든 \<p>태그 선택         |          3           |
|  :nth-last-child(n)  |  p:nth-last-child(2)  | 마지막 자손을 기준으로 시작하여, 부모의 두 번째 자손인 모든 \<p>태그 선택 |          3           |
| :nth-last-of-type(n) | p:nth-last-of-type(2) | 마지막 자손을 기준으로 시작하여, 부모의 두 번째 \<p>태그인 모든 \<p>태그 선택 |          3           |
|   :nth-of-type(n)    |   p:nth-of-type(2)    |     부모 요소의 두 번째 \<p>태그인 \<p>태그 모두 선택     |          3           |
|    :only-of-type     |    p:only-of-type     |       부모 요소의 유일한 \<p>태그인 \<p>태그 선택       |          3           |
|     :only-child      |     p:only-child      |         부모 요소의 유일한 자손인 \<p>태그 선택         |          3           |
|      :optional       |    input:optional     |       어떤 명시된 속성도 없는 \<input>태그 선택        |          3           |
|    :out-of-range     |  input:out-of-range   |      특정 범위를 벗어난 값을 가진 \<input>태그 선택      |          3           |
|      :read-only      |    input:read-only    |     "readonly"속성이 명시된 \<input>태그 선택      |          3           |
|     :read-write      |   input:read-write    |   "readonly"속성이 명시되지 않은 \<input>태그 선택    |          3           |
|      :required       |    input:required     |   "required"이 명시된 속성을 가진 \<input>태그 선택   |          3           |
|        :root         |         :root         |              문서의 root 요소 선택              |          3           |
|     ::selection      |      ::selection      |           유저에 의해 선택된 요소의 부분 선택           |                      |
|       :target        |     #news:target      | 현재 활동하고있는(즉, 엥커 이름이 포함된 URL이 클릭된) #news 요소 선택 |          3           |
|        :valid        |      input:valid      |        유효한 값을 가진 \<input>태그 모두 선택        |          3           |
|       :visited       |       a:visited       |              방문한 모든 링크들 선택               |          1           |


>* first-child와 first-of-type의 차이
>  (하나의 부모는 하나 이상의 자손들을 가질 수 있다. 그 중 오직 하나만 첫 번째 요소가 될 수 있다. 하지만 first-of-type은 html 태그로 구별을 하므로 굳이 첫 번째 자손 요소가 아니더라고 해당될 수 있다는 점이 차이점.(https://stackoverflow.com/questions/24657555/what-is-the-difference-between-first-child-and-first-of-type)
