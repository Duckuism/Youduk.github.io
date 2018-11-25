---
layout: post
title: CSS3 - File Paths
excerpt: "Absolute, Relative File Paths"
categories: [CSS]
link:
comments: true
pinned: true
image:
  feature:
---

######참고자료 :  

1. https://www.w3schools.com/html/html_filepaths.asp
2. https://88240.tistory.com/122

<h3>HTML 파일 경로</h3>

파일 경로는 웹 사이트의 폴더 구조 안의 파일 위치를 설명한다.

파일 경로는 외부 파일들을 링크할 때에 쓰인다.

* Web pages
* Images
* Style Sheets
* JavaScripts

절대 경로(Absolute path) : 절대 경로는 인터넷 파일의 모든 URL이 명시되어 있는 것이다.

\<img src="https://youduk.netlify.com/img/Youduk.jpeg" alt="avatar">

\https://www.google.com, C:\users\document\untitled.jpg

상대 경로(Relative path) : 상대 경로는 현재 페이지에서 상대적으로 가리키는 경로이다.

* / : 루트
* ./ : 현재 위치
* ../ : 현재 위치의 상단 폴더

ex) index.php가 C:\index\a에 위치한다면,
      여기서 / 는 C:,
            ./ 는 a,
            ../ 는 index라는 것.

* 3가지를 간단히 정리하자면,
   * 1  '/'    -> 가장 최상의 디렉토리로 이동한다.(Web root)
   * 2  './'   -> 파일이 현재 디렉토리를 의미한다.
   * 3  '../'  -> 상위 디렉토리로 이동한다

만약 두단계 상위 디렉토리로 이동하려면? '../../'

| <center>Path</center>              | <center>Description</center>             |
| :--------------------------------- | :--------------------------------------- |
| \<img src = "picture.jpg"          | picture.jpg는 현재 페이지와 같은 폴더 안에 위치해 있다.    |
| \<img src = "images/picture.jpg"   | picture.jpg는 현재 폴더 안에 위치된 이미지 폴더 안에 위치해 있다. |
| \<img src = "/images/picture.jpg"> | picture.jpg는 현재 웹의 root에 위치한 이미지 폴더 안에 위치해 있다. |
| \<img src = "../picture.jpg">      | picture.jpg는 현재 폴더로부터 한단계 위 폴더 안에 위치해있다. |
