---
layout: post
title: 네트워킹(Networking)
excerpt: ""
categories: [java]
link:
comments: true
---
### 네트워킹(Networking)

###### 참고 도서 : 자바의 정석(남궁성 저, 도우 출판)

* 흐름을 읽기 위한 단원 목차 훑기

1. 네트워킹
    1. 클라리언트/서버(client/server)
    2. IP주소(IP address)
    3. InetAddress
    4. URL(Uniform Resource Locator)
    5. URLConnection
2. 소켓 프로그래밍
    1. TCP와 UDP
    2. TCP소켓 프로그래밍
    3. UDP소켓 프로그래밍

<h3>1.네트워킹</h3>

네트워킹이란 두 대 이상의 컴퓨터를 케이블로 연결하여 네트워크를 구성하는 것.

<h5>1.1 클라이언트/서버</h5>

'클라이언트/서버'는 컴퓨터간의 관계를 역할로 구분하는 개념이다. 서버(server)는 서비스를 제공하는 컴퓨터(service provider)이고, 클라이언트(client)는 서비스를 사용하는 컴퓨터(service user)가 된다.

서버에 접속하는 클라이언트 수에 따라 하나의 서버가 여러 가지 서비스를 제공하기도 하고 하나의 서비스를 여러 대의 서버로 제공하기도 한다.

서버가 서비스를 제공하기 위해서는 서버프로그램이 있어야 하고 클라이언트가 서비스를 제공받기 위해서는 서버프로그램과 연결할 수 있는 클라이언트 프로그램이 있어야 한다. 일반 PC의 경우 주로 서버에 접속하는 클라이언트 역할을 수행하지만, FTP Serv - U와 같은 FTP서버프로그램이나 Tomcat과 같은 웹서버프로그램을 설치하면 서버역할도 수행할 수 있다.

네트워크를 구성할 때 전용 서버를 두는 것을 서버기반모델(server-based model)이라하고 별도의 전용서버없이 각 클라이언트가 서버역할을 동시에 수행하는 것을 P2P모델(peer-to-peer model)이라 한다.

|  <center>서버기반 모델(server-based model)</center> |  <center>P2P 모델(peer-to-peer model)</center>|
|:--------|:--------|
|* 안정적인 서비스의 제공이 가능하다.<br />* 공유데이터의 관리와 보안이 용이하다. <br />* 서버구축비용과 관리비용이 든다. |* 서버구축 및 운용비용을 절감할 수 있다.<br />* 자원의 활용을 극대화 할 수 있다.<br />* 자원의 관리가 어렵다.<br />* 보안이 취약하다.|

<h5>1.2 IP주소</h5>

* IP주소 : 컴퓨터(호스트,host)를 구별하는데 사용되는 고유한 값

인터넷에 연결된 모든 컴퓨터는 IP주소를 갖는다. IP주소는 4 byte(32bit)의 정수로 구성되어 있으며, 4개의 정수가 마침표를 구분자로 'a,b,c,d'와 같은 형식으로 표현된다. 여기서 a,b,c,d는 부호없는 1 byte값, 즉 0~255사이의 정수이다.

IP주소는 다시 네트워크 주소와 호스트 주소로 나눌 수 있는데, 32bit(4byte)의 IP주소 중에서 네트워크 주소와 호스트 주소가 각각 몇 bit를 차지하는 지는 네트워크를 어떻게 구성하였는지에 따라 달라진다. 그리고 서로 다른 두 호스트의 IP주소의 네트워크 주소가 같다는 것은 두 호스트가 같은 네트워크에 포함되어 있다는 것을 의미한다.

IP주소와 서브넷 마스크를 비트 연산자 '&'로 연산하면 IP주소에서 네트워크 주소만을 뽑아낼 수 있다.

<h5>1.3 InetAddress</h5>

InetAddress는 자바에서 IP주소를 다루기 위해 제공하는 클래스이다.

![Smithsonian Image](http://cfile22.uf.tistory.com/image/13336B3A5036CE0E2A7416)<br />

<h5>1.4 URL(Uniform Resource Locator)</h5>

* URL : 인터넷에 존재하는 여러 서버들이 제공하는 자원에 접근할 수 있는 주소를 표현하기 위한 것. '프로토콜://호스트명:포트번호/경로명/파일명?쿼리스트링#참조'의 형태로 이루어져 있다.

http://www.codechbo.com:80/sample/hello.html?referer=codechobo#index1

* 프로토콜 : 자원에 접근하기 위해 서버와 통신하는데 사용되는 통신규약(http)
* 호스트명 : 자원을 제공하는 서버의 이름(www.codechobo.com)
* 포트번호 : 통신에 사용되는 서버의 포트번호(80)
->HTTP프로토콜에서는 80번 포트를 사용하기 때문에 URL에서 포트번호를 생략하는 경우 80으로 간주한다. 각 프로토콜에 따라 통신에 사용하는 포트번호가 다르며 생략되면 각 프로토콜의 기본 포트가 사용된다.
* 경로명 : 접근하려는 자원이 저장된 서버상의 위치(/sample/)
* 파일명 : 접근하려는 자원의 이름(hello.html)
* 쿼리(query) : URL에서 '?'이후의 부분(refere=codechobo)
* 참조(anchor) : URL에서 '#'이후의 부분(index1)

URL을 다루기 위해 자바에서 제공하는 클래스인 URL클래스의 메서드 목록

![Smithsonian Image](http://cfile30.uf.tistory.com/image/1417C9464F02767605575A)<br />

* URL 객체를 생성하는 방법
URL url = new URL("http://www.codechbo.com/sample/hello.html");
URL url = new URL("www.codechobo.com", "/sample/hello.html");
URL url = new URL("http","www.codechbo.com",80,"/sample/hello.html");

<h5>1.5 URLConnection</h5>

URLConnection은 어플리케이션과 URL간의 통신연결을 나타내는 클래스의 최상위 클래스로 추상클래스이다. URLConnection을 상속받아 구현한 클래스로는 HttpURLConnection과 JarURLConnection이 있으며 URL의 프로토콜이 http프로토콜이라면 openConnection()은 Http URLConnection을 반환한다. URLConnection을 사욯해서 연결하고자하는 자원에 접근하고 읽고 쓰기를 할 수 있다.

URLConnection 클래스의 메서드 목록

![Smithsonian Image](http://cfile27.uf.tistory.com/image/182D79364F0279583277B8)<br />

<h3>2. 소켓 프로그래밍</h3>
