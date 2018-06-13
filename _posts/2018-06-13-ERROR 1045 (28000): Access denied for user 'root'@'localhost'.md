---
layout: post
title: Access denied for user 'root'@'localhost' 
excerpt: "MySQL ERROR"
tags: [Boostcourse]
categories: [MySQL]
link:
comments: true
pinned: true
image:
  feature:
---

## ERROR 해결

```$mysql -uroot```를 입력하니 다음과 같은 에러가 났다.

![](/img/mysqlinstall_4.png)

찾아보니 위와 같은 에러가 나는 이유는 두 가지가 있더라.

1. 비밀번호를 틀리게 입력했을 경우
   1. 비밀번호를 초기화 하는 방법이 있겠다. : http://babytiger.tistory.com/entry/mysql%EC%97%90-%EB%A1%9C%EA%B7%B8%EC%9D%B8%EC%9D%B4-%EC%95%88-%EB%90%A0-%EA%B2%BD%EC%9A%B0
   2. 
2. 정말로 접근 권한 자체가 없을 경우 (이 경우는 보통 sudo를 입력하면 대부분 해결된다.)
   1. root의 db를 전체 삭제했다가 다시 생성하는 방법이 있겠다. 하지만 그다지 좋은 방법이 아니고, 이런 식으로 문제를 해결하면 안 된다. : https://www.wsgvet.com/bbs/board.php?bo_table=web&wr_id=181
   2. 역시나 갓 구글링.. sudo 명령어로 root에 접근 권한을 부여받고, -p 옵션을 이용해서 패스워드를 입력하면 됐다. 
      1. ```$sudo mysql -uroot -p``` 명령어를 입력한다.
      2. 처음 명령어를 입력하는 경우는 아래 그림 처럼 비밀번호를 두 번 요구한다. sudo 명령어에 대한 MacOS 접근 비밀번호와 MySQL의 root 비밀번호이다.
         ![](/img/mysqlinstall_5.png)
      3. 처음에 sudo 명령어에 대한 비밀번호를 입력하여 접근 권한을 부여받으면, 터미널 창을 종료 하지 않고 다시 MySQL을 실행하는 경우에는 아래 이미지 처럼 MySQL의 root 계정에 대한 비밀번호만 입력하면 된다.
         ![](/img/mysqlinstall_6.png)
      4. https://stackoverflow.com/questions/17975120/access-denied-for-user-rootlocalhost-using-password-yes-no-privileges

나는 기존에 MySQLworkbench로 작업한 적이 있어서 workbench를 통해 root 비밀번호를 입력해보니 기존에 내가 입력했던 값이 맞았다. 따라서 두 번째의 원인이라고 생각되어 2-2번의 방법으로 해결했다.