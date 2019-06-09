---

title : "Visual Studio에서 MariaDB 연동하기"
date : 2019-06-09 10:00:00 + 0000
tags: MariaDB, VisualStudio
category: Database

---

# Intro
이번 포스트에서는 Visual Studio에서 MariaDB를 연동하는 방법을 정리하였다.

***

# 1. Visual Studio 웹 개발 도구 설치

Visual Studio가 이미 설치되어 있다고 전제하고 진행하겠다. 아래와 같이 웹 개발 도구를 다운로드 한다.
**[도구] > [도구 및 기능 가져오기] > 웹 개발 다운로드 > [수정]**

![MriaDB1](/assets/images/2019-06-09-MariaDB2/1.png){: width="900" height="700"}

***

# 2. MySQL ODBC Driver 설치 설치

**1) [여기](https://downloads.mysql.com/archives/c-odbc/)에 접속한다.**

**2) 버전에 맞게 Windows용 ODBC Driver를 다운로드 한다.**

![MriaDB2](/assets/images/2019-06-09-MariaDB2/2.png){: width="900" height="700"}

**3) 아래와 같이 ODBC Driver 설치를 진행한다.**

![MriaDB3](/assets/images/2019-06-09-MariaDB2/3.png){: width="900" height="700"}

![MriaDB4](/assets/images/2019-06-09-MariaDB2/4.png){: width="900" height="700"}

![MriaDB5](/assets/images/2019-06-09-MariaDB2/5.png){: width="900" height="700"}

![MriaDB6](/assets/images/2019-06-09-MariaDB2/6.png){: width="900" height="700"}

**4) [제어판] > [시스템 및 보안] > [관리 도구] > [ODBC 데이터 원본] > [시스템 DNS]**

다음과 같은 순서로 ODBC를 추가 해준다.

![MriaDB7](/assets/images/2019-06-09-MariaDB2/7.png){: width="900" height="700"}

![MriaDB8](/assets/images/2019-06-09-MariaDB2/8.png){: width="900" height="700"}

아래와 같이 각 항목을 입력해준다. Test 버튼을 눌렀을 때 "Connection Successful"이 출력되어야 한다.

![MriaDB9](/assets/images/2019-06-09-MariaDB2/9.png){: width="900" height="700"}

***

# 3. Visual Studio에서 사용해보기

**1) [Visual Studio] > [파일] > [새로만들기] > [웹 사이트] > [ASP.NET 빈 웹사이트]**
