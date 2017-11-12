---
layout: post
title: AWT와Applet
excerpt: "기초적인 프로그래밍 학습에 좋은 AWT."
categories: [java]
link:
comments: true
pinned: true
image:
  feature: java.jpg
---
# AWT

###### 참고 자료 : 자바의 정석(남궁성 저, 도우 출판)

1. AWR
    1. AWT란?
      AWT(Abstract Window Toolkit)은 이름에서 알 수 있듯이 Window프로그래밍(GUI프로그래밍)을 하기 위한 도구이다.  AWT는 GUI어플리케이션의 개발에 필요한 여러 개의 관련 패키지와 클래스의 집합으로 구서오디어 있으며, 이들을 이용하면 윈도우와 같은 GUI어플리케이션을 쉽고 편리하게 작성할 수 있다.

    2. AWT의 구성
      패키지명이 'java.awt'로 시작하는 것은 모두 AWT관련 패키지이다. 아래에 소개한 것 외에도 더 많은 AWT관련 패키지가 있지만 java.awt와 java.awt.event패키지만 학습해도 충분하다.      
      메뉴와 관련된 컴포넌트들을 제외한 모든 컴포넌트의 조상은 Componene클래스이고 Component클래스의 조상은 Object클래스이다. Component클래스와 그 자손 클래스들은 윈도우, 스크롤바, 버튼 등 GUI응용프로그램의 화면을 구성하는데 사용되는 클래스들이다. 이들은 AWT컴포넌트 또는 줄여서 컴포넌트라고 부른다.

    | <center>패키지명</center>    | <center>설명</center>                      |
    | :----------------------- | :--------------------------------------- |
    | **java.awt**             | AWT를 이용한 GUI어플리케이션을 작성하는데 필요한 기본적인 클래스와 컴포넌트를 제공한다. |
    | **java.awt.datatranfer** | 여러 어플리케이션 사이의, 또는 단일 어플리케이션 내에서의 데이터 전송을 구현하는데 필요한 클래스와 인터페이스를 제공한다. |
    | **java.awt.dnd**         | GUI의 장점 중의 하나인 끌어놓기(Drag and Drop)기능을 구현하는데 필요한 클래스들을 제공한다. |
    | **java.awt.event**       | GUI어플리케이션에서 발생하는 이벤트를 처리하는데 필요한 클래스와 인터페이스를 제공한다. |
    | **java.awt.font**        | 폰트와 관련된 클래스와 인터페이스를 제공한다.                |
    | **java.awt.image**       | 이미지를 생성하거나 변경하는데 사용되는 클래스를 제공한다.         |
    | **java.awt.print**       | 출력에 관련된 클래스와 인터페이스를 제공한다.                |

    >AWT 일반 컴포넌트의 상속계층도

    ![AWT 일반 컴포넌트의 상속계층도](http://pds14.egloos.com/pds/200901/26/65/a0104265_497d30427d480.gif);
    >AWT 메뉴 컴포넌트의 상속계층도

    ![AWT 메뉴 컴포넌트의 상속계층도](http://pds10.egloos.com/pds/200901/26/65/a0104265_497d3043dff73.gif);

    컴포넌트는 버튼이나 체크박스와 같은 일반적인 컴포넌트와 메뉴와 관련된 메뉴컴포넌트로 나누어진다. Component는 일반적인 컴포넌트의 최상위 조상이며, MenuComponenet는 메뉴관련 컴포넌트들의 최상위 조상이다.

    3. 컴포넌트
      Component는 MenuComponent를 제외한 AWT의 모든 컴포넌트의 조상이고 추상 클래스이다. Componenet에는 컴포넌트들이 가져야 할 공통적인 메서드들을 정의해놓고 있으며, 주로 사용되는 메서드는 다음과 같다.

    | <center>패키지명</center>    | <center>설명</center>                      |
    | ------------------------ | ---------------------------------------- |
    | **입력필요함 다 안함**           | AWT를 이용한 GUI어플리케이션을 작성하는데 필요한 기본적인 클래스와 컴포넌트를 제공한다. |
    | **java.awt.datatranfer** | 여러 어플리케이션 사이의, 또는 단일 어플리케이션 내에서의 데이터 전송을 구현하는데 필요한 클래스와 인터페이스를 제공한다. |
    | **java.awt.dnd**         | GUI의 장점 중의 하나인 끌어놓기(Drag and Drop)기능을 구현하는데 필요한 클래스들을 제공한다. |
    | **java.awt.event**       | GUI어플리케이션에서 발생하는 이벤트를 처리하는데 필요한 클래스와 인터페이스를 제공한다. |
    | **java.awt.font**        | 폰트와 관련된 클래스와 인터페이스를 제공한다.                |
    | **java.awt.image**       | 이미지를 생성하거나 변경하는데 사용되는 클래스를 제공한다.         |
    | **java.awt.print**       | 출력에 관련된 클래스와 인터페이스를 제공한다.                |

    4. 컨테이너
      Component의 자손들 중에 Container와 그 자손들이 있는데, 이들을 컨테이너라고 부른다. 컨테이너는 다른 컴포넌트들을 포함할 수 있어서 Button,Label과 같은 컴포넌트들을 포함할 수 있다. 또한 컴테이너가 컨테이너를 포함할 수도 있다.
          1. 독립적인 컨테이너
            독립적으로 사용될 수 있으며, 다른 컴포넌트나 종속적인 컨테이너를 포함할 수 있다.

      | <center>컨테이너</center> | <center>설명</center>                      |
      | :-------------------- | :--------------------------------------- |
      | **Frame**             | 가장 일반적인 컨테이너로 윈도우와 모양이 같다. titlebar와 크기조절버튼, 닫기버튼을 가지고 있다. 그리고 메뉴를 추가할 수 있다. |
      | **Window**            | Frame의 조상이며, 경계선, titlebar, 크기조절버튼, 닫기 버튼이 없으며, 메뉴도 추가할 수 없다. 단지 컴포넌트를 담을 수 있는 평면공간만을 갖는다. |
      | **Dialog**            | Frame처럼, titlebar와 닫기버튼을 갖고 있지만, 메뉴는 가질 수 없으며 기본적으로 크기를 변경할 수 없다. 주로 프로그램 사용자에게 메세지를 보여주거나, 응답을 받는데 사용한다. |

          2. 종속적인 컨테이너
            독립적으로 사용될 수 없으며, 다른 컨테이너에 포함되어야만 한다.

      | <center>컨테이너</center> | <center>설명</center>                      |
      | :-------------------- | :--------------------------------------- |
      | **Panel**             | 평면공간으로 Frame과 같이 여러 컴포넌트를 담을 수 있으나 단독적으로 사용될 수는 없다. |
      | **ScrollPane**        | Panel과 같은 평면공간이지만, Panel과는 달리 단 하나의 컴포넌트만 포함할 수 있으며 자신보다 큰 컴포넌트가 포함되면 스크롤바가 자동적으로 나타난다. |

        컨테이너에는 여러 개의 오버로딩(overloading)된 add메서드들이 정의되어 있어서, 컴테이너에 단순히 add메서드를 사용하는 것만으로 다른 컴포넌트들을 포함시킬 수 있다. 컨테이너에 포함된 컴포넌트들은 기본적으로 컨테이너에 설정된 배경색(background color)과 전경색(foreground color), 글자체 등의 설정을 그대로 따르게 된다.

        AWT(Abstract Window Toolkit)은 이름에서 알 수 있듯이 Window프로그래밍(GUI프로그래밍)을 하기 위한 도구이다.  AWT는 GUI어플리케이션의 개발에 필요한 여러 개의 관련 패키지와 클래스의 집합으로 구서오디어 있으며, 이들을 이용하면 윈도우와 같은 GUI어플리케이션을 쉽고 편리하게 작성할 수 있다.




* Container의 메서드    

    | <center>메서드<center>                      | <center>설명</center>                |
    | :--------------------------------------- | :--------------------------------- |
    | **Component[] getComponents[]**          | 컨테이너에 포함되어 있는 모든 컴포넌트를 얻는다.        |
    | **Componenet getComponenet(int n)**      | 컨테이너에 n번째로 추가된 컴포넌트를 얻는다.          |
    | **Componenet getComponenetAt(int x, int y)** | 컨테이너의 지정된 위치(x,y)에 있는 컴포넌트를 얻는다.   |
    | **Componenet get(Componenet comp)**      | 컨테이너에 컴포넌트를 추가한다.                  |
    | **void remove(Componenet comp)**         | 컨테이너에서 지정된 컴포넌트를 제거한다.             |
    | **Insets getInsets()**                   | 컨테이너의 경계의 크기를 알 수 있는 Inset객체를 얻는다. |
    | **LayoutManager getLayout()**            | 컨테이너에 설정되어 있는 LayoutManager를 얻는다.  |
    | **void setLayout(LayoutManager mgr)**    | 컨테이너에 LayoutManager를 설정한다.         |



2. AWT의 주요 컴포넌트  

    1. Frame
      GUI프로그래밍의 가장 대표적인 컴포넌트로 다른 컴포넌트들을 포함할 수 있는 컨테이너이다. titlebar와 최대화버튼, 최소화버튼, 닫기버튼이 있으며 크기를 조절할 수 있다.
          1. Frame객체를 하나 만들고, - 생성자에 사용된 String은 Frame의 titlebar에 나타난다.
        ~~~java
            Frame f = new Frame("Login");
        ~~~

          2. 생성된 Frame의 크기를 설정한 다음 - 폭(width):300픽셀(pixel), 높이 200픽셀
        ~~~java
            f.setSize(300,200);
        ~~~

          3. Frame을 화면에 보이도록 한다. - Frame객체를 생성했다고 해서 화면에 보이는 것은 아니고 반드시 setVisible()을 사용해야 화면에 나타난다.
        ~~~java
            f.setVisible
        ~~~

        Frame객체의 설정작업(크기조절)이 모두 끝난 후에 마지막으로 setVisible()을 호출하도록 한다. 만일 setSize() 보다 setVisible(true)를 먼저 호출하면, Frame의 크기가 변겨오디는 과정이, 아주 짧은 시간동안이지만 화면에 보일 것이다. 이렇게 되면, 보기에도 좋지 않을 뿐더러 Frame이 변경될 때마다 화면을 갱신해야하므로 비효율 적이다.

        * setSize()와 setVisible()은 Frame의 조상인 Componenet에 정의된 메서드이다.



    2. Button
    Button은 사용자가 클릭했을 때, 어떤 작업이 수행되도록 할 때 사용된다.
    
    3. Choice
    여러 개의 item이 있는 목록을 보여주고, 그 중에서 한 가지를 선택하도록 할 때 Choice를 사용한다.
    * 기존의 GUI프로그래밍에서는 Choice를 콤보박스(combo box) 또는 드랍다운 리스트박스(drop-down listbox)라고 부른다.
    4. List
    List 역시 Choice처럼 목록 중에서 원하는 항목(item)을 선택할 수 있도록 할 때 사용된다. 그러나 List는 Choice와는 달리, 처음부터 모든 item목록을 보여주며, 목록의 item 중에서 하나 또는 여러 개를 선택하도록 할 수 있다.
    5. Label
    Label을 사용하면 화면에 글자를 표시할 수 있으며, 설명이나 메시지를 화면에 나타내는데 주로 사용된다.
    6. Checkbox
    Checkbox는 boolean과 같이 true/false 또는 on/off와 같이 둘 중의 한 값을 가질 수 있는 컴포넌트다. 또 CheckboxGroup을 이용하면, 여러 가지 값들 중에서 한 가지를 선택할 수 있는 radio button도 만들 수 있다.
    7. TextField
    사용자로부터 값을 입력을 받을 수 있는 컴포넌트이다. 편집이 가능하며 한 줄만 입력할 수 있어서 이름, id, 비밀번호 등 비교적 짧은 값의 입력에 사용된다.
    8. TextArea
    TextArea는 여러 줄의 Text를 입력하거나 보여줄 수 있는 편집가능한 컴포넌트이다. 그리고 스크롤바를 이용해서 실제화면에 보이는 것보다 많은 양의 text를 담을 수 있다.
    9. Scrollbar
    Scrollbar는 사용자가 정해진 범위 내에 있는 값을 쉽게 선택할 수 있도록 해주는 컴포넌트이다. 주로 볼륨설정이나, 속도조절, 색상 선택과 같은 곳에 사용된다.
    10. Canvas
    Canvas는 이름에서 알 수 있듯이 빈 평면 공간을 제공하는 컴포넌트이다. 여기에 그림을 그릴수도 있고, 글자를 적을 수도 있다. 주로 그림을 그리거나 이미지를 위한 공간으로 사용되며, 사용자정의 컴포넌트를 만들 때도 사용된다.
    11. Panel
    Panel은 Frame과 같이 다른 컴포넌트를 자신의 영역 내에 포함시킬 수 있는 컨테이너다. 동시에 Panel 자신이 다른 컨테이너에 포함될 수 있기도 하다. 심지어는 Panel이 Panel에 포함되는 것도 가능하다.
    Panel은 Frame과는 달리 titlebar나 버튼도 없고, 단지 비어있는 평면공간만을 갖는다. Panel도 컨테이너라 자신만의 레이아웃(Layout)을 유지할 수 있어서, Panel을 이용하면 Frame내에서 컴포넌트들의 배치를 다양하게 할 수 있다. 앞으로 레이아웃 관리자에 대해서 배우게 될 텐데, 이 때 Panel이 컴포넌트의 배치에 얼마나 유용하게 사용될 수 있는지 알 수 있다.
    12. ScrollPane
    ScrollPane은 컨테이너이므로, 다른 컴포넌트를 포함시킬 수 있으나 다른 컨테이너들과는 달리 단 하나의 컴포넌트만을 포함시킬 수 있다. 제한된 공간에서 크기가 큰 컴포넌트를 화면에 보여줄 수 있도록 하는데 사용되며, 포함된 컴포넌트의 크기가 ScrollPane 자신보다 큰 경우 스크롤바를 이용해서 볼 수 있게 해준다.
    13. Dialog
    Dialog는 주로 화면에 메세지창을 보여주는데 사용된다. 프로그램의 실행 중에 사용자에게 에러가 발생했음을 알린다던가, 파일을 삭제하기 전에 사용자로부터 응답을 받아야 한다던가 하는데 사용된다.
    Dialog 역시 다른 컴포넌트들을 포함할 수 있는 컨테이너이며, Frame과 유사한 모양을 하고 있다.
    14. FileDialog
    FileDialog는 파일을 열거나 저장할 때 사용되는 Dialog이다. 대부분의 기능들이 이미 구현되어 있기 때문에 따로 코드를 추가하지 않아도 된다.
3. 그 외의 AWT 클래스
    1. Font
    2. Color
4. 메뉴 만들기
    1. 메뉴를 구성하는 컴포넌트
    2. PopupMenu
5. 레이아웃 매니저
    1. 레이아웃 매니저를 이용한 컴포넌트 배치
    2. BorderLayout
    3. FlowLayout
    4. GridLayout
    5. CardLayout
6. 이벤트 처리
    1. 이벤트란?
    2. 이벤트의 발생과 처리
    3. 이벤트 처리 방법
    4. Adapter 클래스
7. AWT의 그래픽
    1. paint()와 Graphics
    2. AWT쓰레드와 repaint()
    3. Image를 이용해서 이미지 출력하기
8. 애플릿(Applet)
    1. 애플릿(Applet)이란?
    2. Applet의 생명주기(Life cycle)와 주요 메서드
    3. Applet의 보안 제약(Security restriction)
    4. Applet과 HTML태그
