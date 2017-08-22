---
layout: post
title: rails에서 template 제대로 적용하기!
excerpt: "rails에서 내가 봤던 demo버전의 js,css를 그대로 적용하기위한 사투"
categories: [rails]
link: http://hashcode.co.kr/questions/2516/ruby-on-rails-template-%EC%A7%88%EB%AC%B8
comments: true

---

###### 이번에 멋쟁이 사자처럼 해커톤을 진행하면서, 서비스를 부각시키기 위해 유료 템플릿을 사용하기로 결정했다. 하지만.. 으잉..? 도대체 왜 css,js파일을 assets 안에 넣었는데 적용이 안되는 거냐고요 ㅠㅠ 

##### 나의 작업 환경 : 운영체제: mac os x, 프레임워크: ruby on rails, ide: Rubymine

##### 전체적인 삽질 순서

1. 마음에 드는 유료 템플릿을 얻었다!! 자, 그럼 나의 서비스 개발을 위해 데모 버전을 한 번 적용시켜볼까?
   오류 내용 : css와 js가 전혀 적용되지 않은 생 html파일만 로딩됨.. 
   레일즈 "꺼져 이새끼야, 너의 미천한 실력으로는 나를 import 할 수 없다. 에셋 공부 더 하고 와라"
   해결 방법 : rails의 asset pipeline에 대한 공식 문서 참조, 인터넷 탐색으로 추가 탐색
   그리고 이 모든 방법들을 다 적용해보면서 새로고침 새로고침...


### 삽질의 시작

프론트엔드를 좋아하는 사람으로 나는 이번 멋쟁이 사자처럼에서 프론트엔드 부분을 맞아 웹서비스 페이지 디자인을 했다.
하지만 얼마 전 한 팀원이 "형, 이런 것도 있네요? 유료템플릿이래요."

![이모티콘](http://mblogthumb2.phinf.naver.net/20131114_233/jhyun4394_1384356056863KJfde_PNG/%BE%C6%C0%CC%C4%DC4.png?type=w2){: .center} <br />
아.. 아니 이런 게 존재했단 말야..?
그에 비하면 내가 개발한 웹서비스 디자인은.. 똥 그자체였다.
한껏 자괴감을 맛본 후 쿨하게 유료 템플릿을 이용해서 커스터마이징을 하기로 결정하고 신나게 쓸 페이지들을 골랐다. 그런데...

?????????????????????
js랑 css가 적용되지 않은 완전 생 html파일만 로딩이 되었다. 충격 그 자체..
분명히 폴더 그대로 옮겼는데 왜 적용이 안되는거지? 

나는 또 삽질에 들어갔다. 이번에는 한 10시간 한 것 같다. 머리가 나쁘면 시간이 낭비된다...

일단 rails의 중요한 기능 중 하나인 asset pipeline을 좀 더 공부해봤다.

일단 제일 빠른 길은 역시 rails 공식 레퍼런스를 참조하는 것!!

(rails 한국어 가이드 에셋 파이프라인 부분: [http://guides.rorlab.org/asset_pipeline.html](http://guides.rorlab.org/asset_pipeline.html))

내가 새롭게 알게된 사실들을 나열하면서 순서대로 과정을 정리해보겠다.

>지식 1. 에셋 파이프라인은 app/assets/ 안에 있는 image,js,css파일을 무조건 탐색해서 모두 저장한 후 맞는 파일을 로드한다.<br />

>지식 2. 1번의 사실을 알고나서 바로 넘어 가면 안되는 것이 에셋은 기본적으로 생성되어 있는 config/images/javascript/stylesheets 폴더를 무조건적으로 탐색하므로, html에서 특정 파일을 참조하기 위한 경로 설정을 할 때에 /assets/stylesheets/bootstrap.css형식이 아니라 /assets/bootstrap.css와 같은 형식으로 경로 설정을 설정을 해주어야한다. 내가 사용했던 html파일의 헤드부분을 보자.

![Smithsonian Image](/img/2017-07-26-5.png)
{: .center}

이 파일은 처음 헤드 부분에서 필요한 모든 css파일을 불러온다. 초기 경로 설정이 href = "css/bootstrap.css"와 같은 형식으로 되어있다. css폴더의 bootstrap.css파일을 참조하겠다는 뜻이다.  

그리고 이 html 파일의 맨 끝에 스크립트 부분을 보자.

![Smithsonian Image](/img/2017-07-26-3.png)
{: .center}

문서가 끝나기 직전에 스크립트 태그를 통해서 js폴더의 jquery.js파일을 참조하겠다고 밝히고 있다.

일단 이 두 가지의 구조를 아는 것이 먼저다. 그렇다면,

>지식 3. html파일 자체에서 css,js 파일을 불러오는데 application.html.erb 파일에서 굳이 또 모든 파일을 불러올 필요가 있을까?

위의 질문은 선뜻 이해가 되지 않을 수도 있다.

아래의 사진을 보자. 

![Smithsonian Image](/img/2017-07-26-16.png)
{: .center}

위의 사진에서 stylesheets_link_tag는 stylesheets안에 있는 css파일들을 application.html.erb파일로 모두 불러오겠다는 얘기이다. 그리고 javascript_include_tag는 js파일들을 모두 불러오겠다는 의미이다. 하지만, 지금 내가 사용하고 있는 html파일은 이 부분이 필요가 없다. 왜? 헤드 부분과 스크립트 부분에서 참조를 하기위한 경로 설정을 해놓고 있기 때문에! 만약 위의 사진에 

{% highlight ruby %}
<%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
{% endhighlight %}

이 부분이 남아있다면, html파일 자체에서 필요한 css,js 파일들을 한 번 불러온 후, application.html.erb에서 또 한 번 불러오는 꼴이 된다.
따라서 기존의 템플릿 css가 중복 적용될 가능성도 있으므로 이 부분을 삭제해준다. (이 부분에 대한 내용은 이견이 있을 수 있다. tag부분에 대한 나의 지식이 적어 이 부분이 꼭 없어야 하는 것인지는 확실하지 않으나, 나의 경우를 기준으로 얘기한다.)

![Smithsonian Image](/img/2017-07-26-17.png)
{: .center}

app/views/layout/application.html.erb 파일은 위 사진과 같은 상태로 비워두면 된다.

그리고 이제 무엇을 해야하는가?! 

> 지식 4. 내가 원하는 템플릿의 파일을 assets 폴더 안에 넣어야 에셋 파이프라인에서 불러올 수 있다.

자 이건 또 무슨 말이냐? 말 그대로이지만 처음해보는 사람에게는 어려울 수 있다.

먼저 내가 받은 유료 템플릿 파일을 열어보면 이런 파일 구조를 가지고 있다.

![Smithsonian Image](/img/2017-07-26-7.png)
{: .center}

이처럼 js, css를 폴더를 만들어서 따로 파일을 분류해 놓았다.

우리는 이 html파일들을 써야하므로 이 파일들을 rails app 프로젝트 파일로 옮겨야 한다.

최대한 기본의 템플릿 구조를 살리기 위해서 폴더 자체를 복사해서 app/assets/stylesheets 폴더 안에 css, sass(안에 scss파일들이 들어있음), less(처음 보는 건데 혹시 몰라서 넣음. 나중에보니 sass 기술과 유사한 언어로써 간결하고 유지보수하기 쉬운 css를 만들게 해주는 언어라고 한다.)폴더를 넣고, 폴더 안에 들어있지 않은 바깥에 있는 모든 css, scss파일들를 넣었다. 그리고 app/assets/javascript폴더 안에 js폴더를 넣었다. 또한 이미지도 그대로 살리기 위해서 app/assets/images 폴더는 위의 사진의 images 폴더로 아얘 대치시켰다.

즉, 전체적인 구조를 보자면

![Smithsonian Image](/img/2017-07-26-18.png)
{: .center}

위와 같이 된 상태이다.

이렇게 내가 사용하고자 하는 템플렛의 css,js 관련 파일들을 모두 rails app project 폴더 안에 assets안의 images,javascript,stylesheets 폴더 안에 넣어 놔야 rails 앱이 사용할 수 있다.

그리고 이제 우리가 사용하고자 하는 파일들의 경로가 바뀐 상태이므로 html파일의 헤드부분과 스크립트 부분에서 경로 설정을 변경해주어야한다.


먼저 헤드부분은

![Smithsonian Image](/img/2017-07-26-5.png)
{: .center}
에서
![Smithsonian Image](/img/2017-07-26-4.png)
{: .center}
와 같이 바꾸고

맨 밑의 스크립트 부분은

![Smithsonian Image](/img/2017-07-26-3.png)
{: .center}

에서

![Smithsonian Image](/img/2017-07-26-2.png)
{: .center}

와 같이 바꾼다.

#### 중요!!! 자신의 파일 경로에 맞춰서 해야한다. 설마 내 파일 트리와 똑같이 하는 사람은 없겠쥬..? html파일에서 사용하는 파일이 어떤 경로에 있는 지 먼저 파악한 후, 그것에 맞춰서 수정을 해줘야하는 것이다. 위에도 말했듯이 assets은 무조건적으로 images, javascript, stylesheets 폴더를 탐색하게 되어있으므로 이 폴더 이름들은 중간에 생략한다. (이 폴더명을 넣어도 되는지 아닌지는 정확하지 않다. 나는 넣지 않았을 때 정상적으로 작동했다.)

이렇게 모든 파일 경로를 변경하고 실행!!!!!!!!!!!

그런데.. 나는 분명히 모든 파일을 넣어놨는데도 적용이 되지 않는다. 도대체 왜..?

오류 내용을 보니 scss파일 안의 변수를 읽을 수 없다는 내용이었다. 크흡.. 그럼 무엇이 잘못 된 것인가..

>지식 5. rails에서 변수가 존재하는 새로운 파일들을 사용하려면 import해야 한다!!

이 부분에 대해 구글링을 하다가 아주 좋은 자료를 발견했다. 

(rails파일 import관련 답변: [http://hashcode.co.kr/questions/2516/ruby-on-rails-template-%EC%A7%88%EB%AC%B8](http://hashcode.co.kr/questions/2516/ruby-on-rails-template-%EC%A7%88%EB%AC%B8))

이 부분을 보면 우리가 assets 안에 파일을 넣은 후 사용하려면, import시켜서 해당 파일을 rails에서 쓸 수 있도록 지정해줘야 한다고 하고 있다.

이 자료를 보고 감은 잡았는데, 도통 어떻게 하는지 몰라 시행착오를 많이 거쳤다. (정확히 말하면 가능한 모든 경우의 수를 대입해봤다고 해야겠다^^)

내 블로그를 참조하시는 분들은 이런 수고를 하지 않으셨으면 하는 마음에서 나의 결과물을 남긴다!

application.html.erb에서 css,js 파일을 tag기능으로 한꺼번에 불러올 때 

먼저 application.css 파일에서 모든 css파일을 모아서 application.html.erb의 tag로 보내주는 것이고,

application.js 파일에서 모든 js파일을 모아서 application.html.erb의 tag로 보내주는 것이다. 

따라서 application.css와 application.js 파일에 import명령을 내려줘야 application.html.erb 파일 혹은 다른 view 파일에서 다른 파일들을 인식해서 사용할 수 있다. 조금 이해하기 어렵다면 그냥 아래와 같이 따라하자.


app/assets/javascript/application.js

초기 상태

![Smithsonian Image](/img/2017-07-26-12.png)
{: .center}

에서

![Smithsonian Image](/img/2017-07-26-10.png)
{: .center}

으로 바꾼다.

//=require_directory ./js는 js안에 든 모든 파일들을 import하겠다는 얘기이다.

![Smithsonian Image](/img/2017-07-26-11.png)
{: .center}

이렇게 바꾼다면 js폴더 안에 jquery.js, plugins.js, function.js 파일을 참조하겠다는 의미와 같다.

하지만 참조하는 파일이 많을수록 복잡해지므로 웬만하면 폴더 참조를 이용하도록 하자.


app/assets/stylesheets/application.css

초기 상태

![Smithsonian Image](/img/2017-07-26-15.png)
{: .center}

에서

![Smithsonian Image](/img/2017-07-26-14.png)
{: .center}

위와 같이 바꾼다.

이 명령어는 css폴더 전체를 import하겠다는 얘기이고, style.css 파일을 import하겠다는 얘기이다.

이렇게 내가 사용할 템플릿의 폴더들을 전부 옮기고 폴더 전체를 import해놓으면, 템플릿 안에 어떤 페이지를 사용하던 js와 css가 모두 적용이 된다.

즉 골라서 쓰기만 하면 된다는 뜻!!

정말 이 흐름을 알기 위해 몇 시간을 소비했는지 모르겠다..

하지만 깔끔하게 적용된 나의 템플릿을 보자면 감탄을 금할 길이 없다.. 낄낄낄

다음 달에 있을 해커톤에 멋진 페이지를 보여줄 수 있기를!!!!





