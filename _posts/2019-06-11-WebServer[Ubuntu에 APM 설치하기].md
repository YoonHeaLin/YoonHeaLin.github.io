---

title : "Ubuntu에 APM(Apache, Php, Mysql) 설치하기"
date : 2019-06-11 10:00:00 + 0000
tags: Apache, PHP, MySQL
category: WebServer

---

# Intro
이번 포스트에서는 Ubuntu에 APM을 설치하는 방법을 정리하였다.

***

# 1. APM(Apache, PHP, MySQL) 이란?

APM이란 Apache + PHP + MySQL의 줄임말로 각 구성 요소는 다음과 같은 역할을 한다.

- Apache HTTP server: 웹 서비스를 제공하는 웹 서버
- PHP: 웹 프로그래밍 언어로, 웹 페이지를 구성
- MySQL: 데이터베이스

APM의 구동 원리는 다음과 같다.

![WebServer0](/assets/images/2019-06-11-WebServer1/0.jpg){: width="900" height="700"}

1. Client가 웹 브라우저에 URL을 이볅하여 원하는 정보를 Server에 요청(Request)하고, Server의 Apache 프로그램이 승인한다
2. Server는 PHP에 스크립트 실행을 요청한다.
3. PHP는 미리 작성된 프로그램을 통해 MySQL에 쿼리를 질의한다.
4. MySQL은 데이터베이스에 저장된 데이터를 PHP에 전송한다.
5. PHP는 데이터베이스에서 가져온 데이터와 PHP 코드를 모두 HTML로 변환하여 Apache에게 전송한다.
6. Apache는 완성된 HTML 파일을 Client에게 응답(Response)한다.

***

# 2. APM 설치 및 실행하기

## 2-1. APM 설치하기

APM을 설치하는 방법은 매우 간단하다. 아래의 명령어 한 줄이면 된다.

```
apt-get -y install lamp-server^
```

중간에 mysql 패스워드를 설정해주면 설치가 완료 된다. `dpkg` 명령어를 통해 APM이 잘 설치되었는지 확인할 수 있다.

```
dpkg -l apache2
dpkg -l php7.0-common
dpkg -l mysql-server
```

## 2-2. APM 실행하기

다음과 같이 APM를 시작하여, 웹 서버를 실행시켜보자.

```
systemctl restart apache2
systemctl enable apache2

systemctl restart mysql
systemctl enable myql
```

localhost로 접근해보면, 웹서버가 정상적으로 동작하고 있는 것을 볼 수 있다.

![WebServer1](/assets/images/2019-06-11-WebServer1/1.PNG){: width="900" height="700"}

***

# 3. PHP 프로그래밍 모듈 동작시키기

다음으로 PHP 프로그래밍 모듈을 동작시켜보자.

```
cd /var/www/html

# phpinfo.php 파일 생성
vi phpinfo.php

# 파일 내에 php 함수를 작성하여, php 모듈이 정상 작동하는지 확인
<?php phpinfo();  ?>

```
![WebServer2](/assets/images/2019-06-11-WebServer1/2.PNG){: width="900" height="700"}

localhost/phpinfo.php 주소로 접속했을때, 아래와 같이 화면에 출력되면 php가 정상적으로 작동하고 있는 것이다.

![WebServer3](/assets/images/2019-06-11-WebServer1/3.PNG){: width="900" height="700"}

***

# 4. XpressEngine을 사용하여 웹 사이트 구축하기

## 4-1. XpressEngine이란?

(작성중)

## 4-2. XpressEngine 설치하기

**1) XpressEngine을 설치하기 위해서 다음과 같이 사전 작업을 진행해준다.**

```
apt-get -y install php php-gd php-xml
```

**2) XpressEngine 설치 파일을 다운로드 한다.**

[Express Engine 설치 사이트](https://xpressengine.com/download)에서 XE Core를 다운로드 한다.

![WebServer4](/assets/images/2019-06-11-WebServer1/4.png){: width="900" height="700"}

**3) 설치 파일을 /var/www/html로 옮기고 압축을 풀어준다.**

```
mv /root/다운로드/xe.zip /var/www/html/
cd /var/www/html/

unzip xe.zip

# 외부 사용자가 xe 서버에 접근할 수 있도록, xe 폴더의 권한을 변경해준다.
chmod 707 xe
```

압축을 풀어준 후에 /var/www/html/xe/modules/board 디렉토리를 확인해보자. 이 디렉토리는 게시판으로 사용된다.

**4) XpressEngine 데이터 베이스를 생성한다.**

```
# root 계정으로 mysql 접속
mysql -u root -p{패스워드}

# xeUser 생성 및 권한 부여
GRANT ALL PRIVILEGES ON xeDB.* TO xeUser@localhost IDENTIFIED BY '{패스워드}';

# mysql 종료
exit

# 새로 생성한 mysql 계정으로 mysql 접속
mysql -u xeUser -p{패스워드}

# xeDB 생성
CREATE DATABASE xeDB;

# mysql 종료
exit
```

**5) XpressEngine 웹 서버에 접속(http://{서버 IP}/xe/)하여 설정을 완료한다.**

아래의 순서에 따라 설정 및 확인을 해주면 된다.

- 한국어 선택
- 사용권 동의
- 설치 조건: 설치가 가능한지 확인
- mysqli

- mysqli 정보 입력
![WebServer5](/assets/images/2019-06-11-WebServer1/5.png){: width="900" height="700"}

- Korea Standard Time, Japan Standard Time 선택
- 관리자 정보 입력

정상적으로 완료되면, 아래와 같이 초기 화면이 출력된다.

![WebServer6](/assets/images/2019-06-11-WebServer1/6.PNG){: width="900" height="700"}

***

이렇게 간단하게 APM을 설치하고 XpressEngine을 이용하여 웹 서버를 운영하는 방법을 알아보았다.
