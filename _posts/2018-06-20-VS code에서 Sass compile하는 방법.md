---
layout: post
title: VS code에서 Sass 컴파일 하기!
excerpt: ""
tags: [VS CODE, Sass]
categories: [VS code]
link:
comments: true
pinned: true
image:
  feature: sass.png
---

# VS CODE에서 Sass 환경설정하고 컴파일하기!



Sass 컴파일러는 대표적으로 3가지가 있습니다.

- VS Code + Live Sass Compiler
- ~~Ruby Gem~~
- ~~Node.js NPM~~

저희는 명령어를 사용하지 않고 간단하게 쓸 수 있는 VS CODE 기반의 Live Sass Compiler를 사용해보겠습니다.



일단 그러려면 VS code와 Chrome을 설치하셔야합니다.

VS code 다운로드 : https://code.visualstudio.com/

Chrome 다운로드 : https://www.google.co.kr/chrome/index.html



모두 설치가 되셨으면 본격적으로 들어가보겠습니다. 먼저 VS Code 에디터에 대한 이해가 조금 필요합니다.



## VS CODE

VS는 이클립스와 같은 IDE처럼 프로젝트를 import하거나 하지 않습니다. 에디터이기 때문에 내가 작업하고자 하는 폴더를 열기만 하면 됩니다.

따라서 새로운 프로젝트를 시작하려면! 

1. 먼저 파일탐색기나 파인더에서 내가 원하는 이름으로, 원하는 위치에 프로젝트 폴더를 만들어놓습니다.
2. 다시 VS code로 돌아와서 만들어 놓은 프로젝트 폴더를 연 다음, 새로운 파일을 만들어서 작업을 시작하면 됩니다.

자 스크린샷을 따라가 볼게요

일단 처음에 vscode를 열면 다음과 같은 화면이 나옵니다.

![](/img/vscode1.png)

일단 저는 finder에 들어가서 제가 원하는 위치에 vscodeProject1이라는 이름으로 폴더를 만들었어요.

![](/img/vscode2.png)

그리고 다시 vscode로 돌아와서 폴더 추가를 누릅니다.

![](/img/vscode3.png)

제가 만든 vscodeProject1 폴더를 찾아서 추가!

![](/img/vscode4.png)

그러면 이렇게 폴더가 VS code에 추가된 것을 볼 수 있습니다. 만약 처음 하시는 분들이라면 작업영역이 제목없음이 아니고 해당 폴더 명으로 되어있습니다. 이전에 여러 폴더를 같이 작업한 적이 있으신 분이라면 저처럼 작업 영역이라고 뜨니, 당황하지마세요.

![](/img/vscode5.png)



### VS code 관련 사용자 설정 변경

그리고 VS code 사용자 설정을 바꾸는 방법을 알아볼게요.

왼쪽 하단에 톱니 바퀴 - 설정 - 사용자 설정에서 설정을 바꿀 수 있습니다.

![](/img/vscode6.png)

왼쪽 기본 사용자 설정에서 JSON 형식으로 되어있는 부분을 복사해서 붙여넣고 값을 바꾸면 사용자 설정이 적용됩니다. sublime text3 와 굉장히 유사하네요. 맨 마지막 줄 끝에 ','를 남겨놓아도 인식하는 걸 볼 수 있습니다.

아래 이미지 처럼요!

![](/img/vscode7.png)



### VS code확장 프로그램

그리고 먼저 편의성을 돕기 위해 확장프로그램을 설치합니다.

확장프로그램을 설치하는 방법은 다음과 같습니다. 왼쪽 메뉴 중에서 맨 아래 네모난 메뉴를 클릭합니다. 그러면 다음과 같이 확장프로그램 목록 검색, 설치된 목록, 권장 목록이 나옵니다. 검색 부분에서 자신이 원하는 검색어를 입력하고 관련 확장프로그램을 설치하면 됩니다.

![](/img/vscode8.png)

#### HTML/CSS 관련 확장 프로그램 (추천)

- color highlight : css에서 컬러를 눈으로 볼 수 있게 가시화해줍니다.
- prettier : shift + alt + f로 태그를 예쁘게 정렬해줍니다.

#### 테마/아이콘 관련 확장 프로그램 (추천)

vs code는 테마와 파일 아이콘도 쉽게 변경이 가능합니다.

왼쪽 아래 톱니바퀴 메뉴에서 색 테마를 누르면 선택할 수 있는 테마를 볼 수 있습니다. 방향키로 바꿔가면서 미리보기를 할 수 있습니다. 그리고 맨 아래 '추가 색 테마 설치…'를 누르면 확장프로그램 탭에서 테마들을 검색하여 보여줍니다. 원하는 테마를 설치하고 다시 로드를 누른다음, 다시 왼쪽 아래 톱니바퀴를 누르고 색 테마를 선택해서 설치한 테마로 변경하면 됩니다.

![](/img/vscode9.png)

![](/img/vscode10.png)



#### Sass관련 **필수** 확장 프로그램 (필수)

Sass 컴파일을 하기 위해서는 필수적으로 확장프로그램이 필요합니다.

다음과 같이 확장 프로그램 탭에서 Sass 라고 검색해주세요.

![](/img/vscode11.png)

그리고 아래 세 가지 확장프로그램을 설치합니다.

- Sass
  ![](/img/vscode12.png)
- Live Sass Compiler
  ![](/img/vscode13.png)
  - Live Sass Compiler를 설지하면 Live Server를 확장프로그램이 같이 설치됩니다.
    - html 파일을 만들고 마우스 우클릭 - Open with Live Server 를 누르면 변경사항이 실시간으로 반영이 되는 브라우저가 열립니다. 아래 Port : 5500 이라고 적힌 아이콘이 생성됩니다. 5500포트에서 실시간 미리보기 server를 열고 있다는 얘기입니다.
      ![](/img/vscode16.png)
    - 만약 port 에러가 나면 Live Server의 default port를 이미 다른 프로그램에서 사용하고 있다는 얘기이므로 port 설정을 바꿔주면 됩니다. (왼쪽 하단 톱니바퀴 - 설정 - 사용자 설정 - 맨 마지막출에 ```"liveServer.settings.port":0``` 을 추가하고 저장! 다시 Open with Live Server를 누르면 port 번호가 안 쓰는 port 번호로 랜덤으로 생성되면서 열리는 것을 확인할 수 있습니다.) 
    - 여러 브라우저(IE, Chrome, Firefox)에서 같은 주소를 띄워놓아도 변경사항이 동시에 적용됩니다.
    - 여러 탭이 열렸을 때는 새로 열린 탭만 Live Server가 적용되고 이전 탭들은 실시간으로 적용되지 않습니다. 즉, Live Server가 되는 탭은 각 브라우저 별로 하나씩만 가능한거죠. 이전 탭들은 새로 고침하면 최신 변경사항으로 바뀝니다.
    - MacOS 같은 경우는 command+s를 두 번 눌러야 변경사항이 반영이 되는 것 같습니다.
- Sass Lint
  ![](/img/vscode14.png)



### Sass 관련 설정

자 이제 모든 준비를 마쳤으니 Sass를 컴파일 해볼게요.

설치한 Live Sass Compiler로 Sass 파일을 Css로 변환하겠습니다.

1. Proejct폴더의 root 위치에서 새 폴더 추가 버튼을 누르고 sass폴더를 만듭니다.
   ![](/img/vscode17.png)
2. 그리고 그 안에 scss확장자를 가진 파일을 만듭니다.
   ![](/img/vscode18.png)
   ![](/img/vscode19.png)
3. 이 파일을 열면 VS code 아래 이미지처럼 port 아이콘 왼쪽에 watch sass라는 아이콘이 생기는데, 이 아이콘을 누르면 Live Sass Compiler가 우리가 연 scss 파일을 css로 컴파일해서 sass폴더에 생성해줍니다.
   ![](/img/vscode20.png)
   ![](/img/vscode21.png)
4. console창 맨 윗 줄에 compiling이라고 뜨고, 맨 아래 줄에 Watching이라고 뜨고 있으므로 scss 파일을 변경하고 저장을 하면 바로바로 css로 컴파일이 됩니다.
   ![](/img/vscode22.png)
5. 한 번 확인해볼게요. 먼저 scss파일과 css파일을 양쪽에 열어두겠습니다. 그리고 scss 파일에 원하는 코드를 적습니다.
   ![](/img/vscode23.png)
6. 그리고 저장을 하면? css 파일이 자동으로 컴파일 되는 것을 볼 수 있습니다.
   ![](/img/vscode24.png)
7. 그리고 마지막으로 우리가 작성할 html파일에서 컴파일 된 css파일을 link를 걸어주면, 원하는 style이 DOM에 반영됩니다.
   ![](/img/vscode25.png)
   ![](/img/vscode26.png)
8. Html, css, sass 파일 중 하나라도 바꾼 후 저장을하면 Live Server가 계속 실시간으로 반영을 합니다.
9. 이제 컴파일 하는 것을 완료했으니, 아래와 같이 Sass 문법을 사용해서 scss파일을 수정해보세요!
   ![](/img/vscode27.png)



VS code에서 Sass 컴파일 하는 방법을 알아봤습니다. 막히시는 부분이나 궁금하신 부분이 있으면 댓글, 메시지 부탁드려요 :-)