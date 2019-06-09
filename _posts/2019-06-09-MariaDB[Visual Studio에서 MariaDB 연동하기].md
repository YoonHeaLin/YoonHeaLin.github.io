---

title : "Visual Studio에서 MariaDB 연동하기"
date : 2019-06-09 10:00:00 + 0000
tags: MariaDB, VisualStudio
category: Database

---

# Intro
이번 포스트에서는 Visual Studio에서 MariaDB를 연동하는 방법을 정리하였다.

***

# 1. Visual Studio에 웹 개발 도구 설치

**1) [도구] > [도구 및 기능 가져오기] > 웹 개발 다운로드 > [수정]**

![MriaDB1](/assets/images/2019-06-09-MariaDB2/1.png){: width="900" height="700"}

**2) 아래와 같이 버전에 맞게 선택해준다.**

![MriaDB1](/assets/images/2019-06-09-MariaDB/1.png){: width="900" height="700"}

**3) Here are the commands to run to install MariaDB on your Ubuntu system: 의 명령어를 복사하여 붙여넣는다.**

![MriaDB2](/assets/images/2019-06-09-MariaDB/2.png){: width="900" height="700"}

```
sudo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64,arm64,i386,ppc64el] http://ftp.kaist.ac.kr/mariadb/repo/10.1/ubuntu xenial main'
```

![MriaDB3](/assets/images/2019-06-09-MariaDB/3.png){: width="900" height="700"}

***

# 2. MariaDB 설치

**1) MariaDB를 설치한다.**

```
apt-get update
apt-get -y install mariadb-server mariadb-client
```

**2) 패스워드를 입력하고 <확인>을 눌러준다.**

![MriaDB4](/assets/images/2019-06-09-MariaDB/4.png){: width="900" height="700"}

**3) MariaDB를 시작시킨다.**

```
systemctl restart mysql
systemctl status mysql
```

`mysql`을 입력하면 다음과 같이 mariadb로 접속되는 것을 볼 수 있다.

![MriaDB5](/assets/images/2019-06-09-MariaDB/5.png){: width="900" height="700"}

***

# 3. 외부에서 MariaDB 접속하기

**1) MariaDB 외부 접속 허용을 위해 bind-address를 수정해준다.**

/etc/mysql/my.cnf 경로로 접속하여 아래와 같이 bind-address 부분을 주석 처리해준다.

![MriaDB6](/assets/images/2019-06-09-MariaDB/6.png){: width="900" height="700"}

MariaDB를 재시작해준다.

```
systemctl restart mysql
```

**2) User 정보를 수정해준다.**

```
# MariaDB에 접속
mysql -u root -p

# mysql 전환
use mysql;

# 접속 정보 확인(아래의 표가 출력된다.)
SELECT user, host FROM user WHERE user NOT LIKE '';
+------------------+-----------+
| user             | host      |
+------------------+-----------+
| root             | 127.0.0.1 |
| root             | ::1       |
| debian-sys-maint | localhost |
| root             | localhost |
| root             | server    |
+------------------+-----------+
```

이제 외부에서 접속할 user를 생성하고 권한을 부여해주자.

```
# rin_gu라는 user를 생성하고 권한 부여 (아래와 같이 출력되면 잘 설정된 것이다.)
GRANT ALL PRIVILEGES ON *.* TO rin_gu@'%' IDENTIFIED BY '1234';
Query OK, 0 rows affected (0.00 sec)
```

**3) 접속하려는 외부 서버에 MariaDB client 설치**

**4) 외부에서 접속**

```
mysql -h {MariaDB server IP} -u {user} -p
ex) mysql -h 192.168.111.100 -u rin_gu -p
```
