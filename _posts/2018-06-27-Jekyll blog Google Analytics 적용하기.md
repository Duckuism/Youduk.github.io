---
layout: post
title: Jekyll Blog Google Analytics 적용하기
excerpt: ""
tags: [TIL]
categories: [TIL]
link:
comments: true
pinned: true
image:
  feature: TIL.png
---

안녕하세요!

오늘은 지킬 블로그에서 방문자 수와 여러가지 정보를 조회하기 위해 Google Analytic를 적용하는 방법을 알아보겠습니다. 굉장히 간단합니다.

회원 가입을 위해 

https://www.google.com/analytics/

위의 사이트에 방문하여 계정을 만듭니다. (gmail 계정이 있으시다면 로그인을 하시고, 없으시다면 계정 만들기를 통해 gmail 계정을 만드셔야 합니다.)

![스크린샷 2018-06-27 오후 3.15.46](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.15.46.png)

저는 기존의 gmail계정으로 로그인을 했습니다.

그러면 위와 같은 화면을 보실 수 있습니다.

sign up을 눌러볼까요?

![스크린샷 2018-06-27 오후 3.27.05](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.27.05.png)

다음과 같은 화면이 나옵니다.

지킬 블로그에 적용을 할 것이기 때문에 Website를 클릭하고 Account Name은 저 같은 경우 그냥 이메일 주소로 똑같이 지정했습니다.

Website Name에는 원하는 블로그 이름을 넣으시고, Website URL 부분에 블로그 주소를 넣습니다. 그리고 industry category에서 블로그 주제에 맞는 산업군을 선택한 후, reporting time zone에서 South Korea를 찾아서 선택합니다. 아래 선택사항은 원하는 대로 설정합니다. (참고로 저는 그냥 귀찮아서 다 선택해놨습니다.)![스크린샷 2018-06-27 오후 3.30.08](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.30.08.png)

그리고 들어가면 위와 같은 화면이 나옵니다.

범용 사이트 태그라고 되어있는 부분에 script태그로 감싸진 코드가 있죠? 이 부분을 복사합니다.

설명에 보면 추적할 모든 웹페이지의 head 부분에 넣으라고 나와있습니다. 저희는 블로그 전체를 추적할 것이기 때문에 모든 레이아웃의 최상단인 파일(보통 jekyll blog의 경우 default.html)의 head 부분에 붙여넣겠습니다. 제 블로그는 default.html이 head.html을 include하는 형식이므로 head.html의 맨 앞에 붙여넣었습니다.

![스크린샷 2018-06-27 오후 3.36.40](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.36.40.png)

![스크린샷 2018-06-27 오후 3.36.40-0081429](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.36.40-0081429.png)

자 이제 거의 다 되었습니다. 이제 jekyll 블로그를 github에 push합니다. 그리고 rendering이 완료 될 때까지 조금 기다렸다가 블로그에 접속한 후 개발자도구를 열고 network 탭을 클릭하여 analytics.js가 제대로 나오는지 확인합니다.

![스크린샷 2018-06-27 오후 3.40.48](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.40.48.png)

 다시 google analytics로 돌아가 테스트 트래픽 전송을 누릅니다.![스크린샷 2018-06-27 오후 3.38.44](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.38.44.png)

그러면 새로운 탭에 블로그 페이지가 열리고, 다음과 같이 상태가 바뀝니다.![스크린샷 2018-06-27 오후 3.43.17](/Users/Duck/Project/Youduk.github.io/_posts/assets/스크린샷 2018-06-27 오후 3.43.17.png)

이제 GA가 제대로 적용이 되는 걸 확인했네요!