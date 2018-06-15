---
layout: post
title: Starting MySQL.Manager of pid-file quit without updating
excerpt: "MySQL"
tags: [Boostcourse]
categories: [MySQL]
link:
comments: true
pinned: true
image:
  feature: mysql.jpg
---

또한 mysql.server start 명령어도 입력 시에 다음과 같은 에러가 났다. 

![](/img/mysqlinstall_3.png)

이제 또 해결 방법을 찾아본다. 아래의 블로그에 보니 에러 원인은 기본 실행 계정이 달라진 것이 원인이라고 한다.

https://blog.hannal.com/2010/5/mysql_starting_error_about_permission_problem/

따라서 권한을 해결하기 위해 나의 root 계정이 어디에 있는지를 알아야했다. 아래 포스팅에서 그 방법을 찾았다.

https://stackoverflow.com/questions/17968287/how-to-find-the-mysql-data-directory-from-command-line-in-windows

다음과 같이 입력한다. 

```$sudo mysql -uroot -p -e 'SHOW VARIABLES WHERE Variable_Name LIKE "%dir"' ```

아래 이미지 처럼 MySQL의 root 계정이 위치한 폴더 트리가 보여진다. 

![](/img/mysqlinstall_7.png)

/usr/local/etc/my.cnf

위 에러는 해결하다가 다른 실행방법이 있으므로 일단 Homebrew로 실행하기로 했다.