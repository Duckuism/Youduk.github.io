---
layout: post
title: AWT&Applet
excerpt: "기초적인 프로그래밍 학습에 좋은 AWT."
categories: [java]
link:
---

# AWT

###### 참고 자료 : 자바의 정석(남궁성 저, 도우 출판)

1. AWR
    1. AWT란?
    AWT(Abstract Window Toolkit)은 이름에서 알 수 있듯이 Window프로그래밍(GUI프로그래밍)을 하기 위한 도구이다.  AWT는 GUI어플리케이션의 개발에 필요한 여러 개의 관련 패키지와 클래스의 집합으로 구서오디어 있으며, 이들을 이용하면 윈도우와 같은 GUI어플리케이션을 쉽고 편리하게 작성할 수 있다.

    2. AWT의 구성
    패키지명이 'java.awt'로 시작하는 것은 모두 AWT관련 패키지이다. 아래에 소개한 것 외에도 더 많은 AWT관련 패키지가 있지만 java.awt와 java.awt.event패키지만 학습해도 충분하다.      
    메뉴와 관련된 컴포넌트들을 제외한 모든 컴포넌트의 조상은 Componene클래스이고 Component클래스의 조상은 Object클래스이다. Component클래스와 그 자손 클래스들은 윈도우, 스크롤바, 버튼 등 GUI응용프로그램의 화면을 구성하는데 사용되는 클래스들이다. 이들은 AWT컴포넌트 또는 줄여서 컴포넌트라고 부른다.
        |  <center>패키지명</center> |  <center>설명</center>|
        |--------|--------|
        |**java.awt** |AWT를 이용한 GUI어플리케이션을 작성하는데 필요한 기본적인 클래스와 컴포넌트를 제공한다.|
        |**java.awt.datatranfer** |여러 어플리케이션 사이의, 또는 단일 어플리케이션 내에서의 데이터 전송을 구현하는데 필요한 클래스와 인터페이스를 제공한다.|
        |**java.awt.dnd** |GUI의 장점 중의 하나인 끌어놓기(Drag and Drop)기능을 구현하는데 필요한 클래스들을 제공한다.|
        |**java.awt.event** |GUI어플리케이션에서 발생하는 이벤트를 처리하는데 필요한 클래스와 인터페이스를 제공한다.|
        |**java.awt.font** |폰트와 관련된 클래스와 인터페이스를 제공한다.|
        |**java.awt.image** |이미지를 생성하거나 변경하는데 사용되는 클래스를 제공한다.|
        |**java.awt.print** |출력에 관련된 클래스와 인터페이스를 제공한다.|<br />
        >AWT 일반 컴포넌트의 상속계층도
        ![AWT 일반 컴포넌트의 상속계층도](http://pds14.egloos.com/pds/200901/26/65/a0104265_497d30427d480.gif)
        >AWT 메뉴 컴포넌트의 상속계층도
        ![AWT 메뉴 컴포넌트의 상속계층도](http://pds10.egloos.com/pds/200901/26/65/a0104265_497d3043dff73.gif)
        컴포넌트는 버튼이나 체크박스와 같은 일반적인 컴포넌트와 메뉴와 관련된 메뉴컴포넌트로 나누어진다. Component는 일반적인 컴포넌트의 최상위 조상이며, MenuComponenet는 메뉴관련 컴포넌트들의 최상위 조상이다.

    3. 컴포넌트
    Component는 MenuComponent를 제외한 AWT의 모든 컴포넌트의 조상이고 추상 클래스이다. Componenet에는 컴포넌트들이 가져야 할 공통적인 메서드들을 정의해놓고 있으며, 주로 사용되는 메서드는 다음과 같다.
        |  <center>패키지명</center> |  <center>설명</center>
        |--------|--------|
        |**입력필요함 다 안함** |AWT를 이용한 GUI어플리케이션을 작성하는데 필요한 기본적인 클래스와 컴포넌트를 제공한다.|
        |**java.awt.datatranfer** |여러 어플리케이션 사이의, 또는 단일 어플리케이션 내에서의 데이터 전송을 구현하는데 필요한 클래스와 인터페이스를 제공한다.|
        |**java.awt.dnd** |GUI의 장점 중의 하나인 끌어놓기(Drag and Drop)기능을 구현하는데 필요한 클래스들을 제공한다.|
        |**java.awt.event** |GUI어플리케이션에서 발생하는 이벤트를 처리하는데 필요한 클래스와 인터페이스를 제공한다.|
        |**java.awt.font** |폰트와 관련된 클래스와 인터페이스를 제공한다.|
        |**java.awt.image** |이미지를 생성하거나 변경하는데 사용되는 클래스를 제공한다.|
        |**java.awt.print** |출력에 관련된 클래스와 인터페이스를 제공한다.|

    4. 컨테이너
    Component의 자손들 중에 Container와 그 자손들이 있는데, 이들을 컨테이너라고 부른다. 컨테이너는 다른 컴포넌트들을 포함할 수 있어서 Button,Label과 같은 컴포넌트들을 포함할 수 있다. 또한 컴테이너가 컨테이너를 포함할 수도 있다.
        1. 독립적인 컨테이너
        독립적으로 사용될 수 있으며, 다른 컴포넌트나 종속적인 컨테이너를 포함할 수 있다.

            |  <center>컨테이너</center> |  <center>설명</center>
            |--------|--------|
            |**Frame** |가장 일반적인 컨테이너로 윈도우와 모양이 같다. titlebar와 크기조절버튼, 닫기버튼을 가지고 있다. 그리고 메뉴를 추가할 수 있다.|
            |**Window** |Frame의 조상이며, 경계선, titlebar, 크기조절버튼, 닫기 버튼이 없으며, 메뉴도 추가할 수 없다. 단지 컴포넌트를 담을 수 있는 평면공간만을 갖는다.|
            |**Dialog** |Frame처럼, titlebar와 닫기버튼을 갖고 있지만, 메뉴는 가질 수 없으며 기본적으로 크기를 변경할 수 없다. 주로 프로그램 사용자에게 메세지를 보여주거나, 응답을 받는데 사용한다.|
        2. 종속적인 컨테이너
        독립적으로 사용될 수 없으며, 다른 컨테이너에 포함되어야만 한다.

            |  <center>컨테이너</center> |  <center>설명</center>
            |--------|--------|
            |**Panel** |평면공간으로 Frame과 같이 여러 컴포넌트를 담을 수 있으나 단독적으로 사용될 수는 없다.|
            |**ScrollPane** |Panel과 같은 평면공간이지만, Panel과는 달리 단 하나의 컴포넌트만 포함할 수 있으며 자신보다 큰 컴포넌트가 포함되면 스크롤바가 자동적으로 나타난다.|   
              컨테이너에는 여러 개의 오버로딩(overloading)된 add메서드들이 정의되어 있어서, 컴테이너에 단순히 add메서드를 사용하는 것만으로 다른 컴포넌트들을 포함시킬 수 있다. 컨테이너에 포함된 컴포넌트들은 기본적으로 컨테이너에 설정된 배경색(background color)과 전경색(foreground color), 글자체 등의 설정을 그대로 따르게 된다.
AWT(Abstract Window Toolkit)은 이름에서 알 수 있듯이 Window프로그래밍(GUI프로그래밍)을 하기 위한 도구이다.  AWT는 GUI어플리케이션의 개발에 필요한 여러 개의 관련 패키지와 클래스의 집합으로 구서오디어 있으며, 이들을 이용하면 윈도우와 같은 GUI어플리케이션을 쉽고 편리하게 작성할 수 있다.




* Container의 메서드    
    |  <center>메서드<center> |  <center>설명</center>
    |--------|--------|
    |**Component[] getComponents[]** |컨테이너에 포함되어 있는 모든 컴포넌트를 얻는다.|
    |**Componenet getComponenet(int n)** |컨테이너에 n번째로 추가된 컴포넌트를 얻는다.|              |**Componenet getComponenetAt(int x, int y)** |컨테이너의 지정된 위치(x,y)에 있는 컴포넌트를 얻는다.|   |**Componenet get(Componenet comp)** |컨테이너에 컴포넌트를 추가한다.|
    |**void remove(Componenet comp)** |컨테이너에서 지정된 컴포넌트를 제거한다.|              |**Insets getInsets()** |컨테이너의 경계의 크기를 알 수 있는 Inset객체를 얻는다.|              |**LayoutManager getLayout()** |컨테이너에 설정되어 있는 LayoutManager를 얻는다.|**void setLayout(LayoutManager mgr)** |컨테이너에 LayoutManager를 설정한다.|



2. AWT의 주요 컴포넌트  
    2.1 Frame
    2.2 Button
    2.3 Choice
    2.4 List
    2.5 Label
    2.6 Checkbox
    2.7 TextField
    2.8 TextArea
    2.9 Scrollbar
    2.10 Canvas
    2.11 Panel
    2.12 ScrollPane
    2.13 Dialog
    2.14 FileDialog
3. 그 외의 AWT 클래스
    3.1 Font
    3.2 Color
4. 메뉴 만들기
    4.1 메뉴를 구성하는 컴포넌트
    4.2 PopupMenu
5. 레이아웃 매니저
    5.1 레이아웃 매니저를 이용한 컴포넌트 배치
    5.2 BorderLayout
    5.3 FlowLayout
    5.4 GridLayout
    5.5 CardLayout
6. 이벤트 처리
    6.1 이벤트란?
    6.2 이벤트의 발생과 처리
    6.3 이벤트 처리 방법
    6.4 Adapter 클래스
7. AWT의 그래픽
    7.1 paint()와 Graphics
    7.2 AWT쓰레드와 repaint()
    7.3 Image를 이용해서 이미지 출력하기
8. 애플릿(Applet)
    8.1 애플릿(Applet)이란?
    8.2 Applet의 생명주기(Life cycle)와 주요 메서드
    8.3 Applet의 보안 제약(Security restriction)
    8.4 Applet과 HTML태그
