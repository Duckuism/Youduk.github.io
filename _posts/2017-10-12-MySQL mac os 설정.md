---
layout: post
title: MySQL mac os 설정 방법
excerpt: "참고 자료와 정리"
categories: [SQL]
comments: true
---


<h5>how to start mysql server in mac os</h5>

https://github.com/helloheesu/SecretlyGreatly/wiki/%EB%A7%A5%EC%97%90%EC%84%9C-mysql-%EC%84%A4%EC%B9%98-%ED%9B%84-%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0

<h5>맥 터미널에서 mysql실행하기</h5>

https://stackoverflow.com/questions/26554818/using-mysql-in-the-command-line-in-osx-command-not-found

<h5>The server quit without updating PID file 에러.</h5>

http://bryan7.tistory.com/476

http://bellsilver7.tistory.com/28

https://stackoverflow.com/questions/9624774/after-mysql-install-via-brew-i-get-the-error-the-server-quit-without-updating

https://stackoverflow.com/questions/4444861/pid-error-on-mysql-server-start

<br />
해결방법이 약간 서로 다른데; 세번째가 가장 자세하다.

위에 질문들을 통해 mysql을 homebrew로 설치하고, 경로를 설정했다.

그리고 최종으로는 공식 홈페이지의 방법으로 command line client로 접속할 수 있었다.<br />

https://dev.mysql.com/doc/mysql-getting-started/en/#mysql-getting-started-connecting <br />

<h5>mysql 캐릭터셋 바꾸는 명령어.</h5>

http://develop.sunshiny.co.kr/385

set character_set_server = utf8;<br />



<h5>No mapping found for HTTP request with URI 에러</h5>

http://acua.tistory.com/entry/No-mapping-found-for-HTTP-request-with-URI <br />
