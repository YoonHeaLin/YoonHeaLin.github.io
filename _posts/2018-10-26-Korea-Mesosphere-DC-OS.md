---

title : "Korea Mesosphere DC/OS"
date : 2018-10-26 10:00:00 + 0000
tags: seminar
category: seminar

---

# Intro
---

Korea Mesosphere DC/OS Conference 참석

# Main Session By SAM CHEN(REGIONAL VP OF APJATMESOSPHERE)
---

### High Density Multiple Kubernetes
**하나의 OS에 2개 이상의 쿠버네티스를 올릴 수 있다** 이는 다음과 같은 효과를 가진다.

- 이러한 방식으로 환경을 구성할 경우, 최대 50%의 리소스 절약이 가능하다.
- 두개의 쿠버네티스는 완전히 독립된 환경을 가지기 때문에 클러스터 간의 교섭없이 작동 가능하다.
- 어떤 클러스터를 제대로 작동할지만 결정하면, 그 이후에 리소스 관리를 고민하지 않아도 된다.

# MSA With DC/OS By 이용혁 이사(KBSYS)
---
이번 세션에서는 왜 MSA를 사용하는지, 사용해야 하는지를 논의하였다.

### Monolithic Architecture의 문제점
- 서비스가 너무 커져서 유지보수가 어려움
- 서비스 분리가 필요할 떄 분리의 어려움
- 연계 시스템 변경이 필요할 시 전체 시스템 재구축
- 연계 시스템 장애시 관련된 전체 서비스 통일 장애
- 배초 과정 후 저네 통합 테스트 및 QA 필수 필요
- 기존 개발된 소스를 변경할 수 없으며, 만약 변경시 전체 재구축이 더 손쉬울 수 있음

### 기업 사례

(사진)

- Netfilx
![Netfilx](/assets/images/2018-10-26-DCOS/IMG_2437.JPG)

- Uber
![Uber](/assets/images/2018-10-26-DCOS/IMG_2438.JPG)

- airbnb
![airbnb](/assets/images/2018-10-26-DCOS/IMG_2439.JPG)

- eBay
![eBay](/assets/images/2018-10-26-DCOS/IMG_2440.JPG)

### MSA 왜 할까?
서비스를 빠르고 안정적으로 **관리** 하기 위해서이다.
MSA(Micro Servie Architecture)의 의미는 **Managed Servie Architecture** 라고 할 수 있다.

그렇다면 누가 관리할까? **WORK** 의 영역에는 담당(Business)/개발(Develop)/운영(System)이 있다.
이를 위해 실제로 필요한 것은 **COLLABORATION** 으로, 담당(Domain)/개발(App)/운영(Infra)이다. 도메인에 적합한 개발과 도메인에 맞게 운영할 수 있는 인프라가 중요한 것이다.

**어떻게 협업을 할 수 있을까?**
**MSA** 를 통해 가능하다. MSA 환경을 제대로 구축하기 위해서는, 소통이 가능(2 Pizzas)해야 하며, 독립적(Container)이여야 하고, 지속가능(CI/CD)해야 한다.

**DC/OS는 MSA에 어떤 도움을 줄 수 있을까?**
- 환경 설정(Multi Tenancy)
팀별 독립적인 개발환경을 제공하며, 그룹별 독립적인 운영 환경을 제공한다. DC/OS는 자원의 격리를 통해 서비스간 영향을 주지 않도록 환경 설정을 돕는다.
![환경 설정](/assets/images/2018-10-26-DCOS/IMG_2441.JPG)

- 컨테이너(Container Orchestration)
복잡한 파이프라이을 통합하고, 자동화를 통해 빠른 배포를 지원한다.
![컨테이너](/assets/images/2018-10-26-DCOS/IMG_2442.JPG)

- 쉬운 운영(LoadBalance, ScaleOut, ...)
기존에는 고급 인력들이 서비스를 정상적으로 **실행** 시키는 것, 즉 프로그램이 제대로 설치되고 배포되었는지를 확인하는 작업에 투입되었다.  DC/OS는 Deploy, Scale, Monitor 등을 지원하므로써, 기술자들이 **좋은 서비스** 를 고민할 수 있게 한다.
![쉬운 운영](/assets/images/2018-10-26-DCOS/IMG_2443.JPG)


# One Year With DC/OS By 민영근 박사(AJ 네트윅스)
---

### 구축

### 운영

### 서비스 중인 시스템 소개

### 결론


# 마이크로서비스 이야기 By 손욱동 수석(매그나칩반도체)
---

### 시장 기술의 변화
Physical -> Virtual -> ....Container.... -> Private Cloud -> Public Cloud

### Micro Service

(사진)

IProduct라는 사이트를 만드는 것을 계기로 시작하게 되었다.
이전에는 이메일, ftp, 외장하드로 주고 받았으나, ?

Micro Service를 도입하기 위해서, 서비스를 작은 단위로 분리하는 것을 기획하였고, 사용자 관리, 파일 관리, 전자 결재, 게시판 관리로 서비스를 분리하였다.

초기 서비스 분리, 하드웨어 구성에는 어려움이 없었다.

DB를 받아왔는데, 하나도 분리되어 있지 않았음
그러나 발표자는 디비부터(처음부터) 서비스까지(끝까지) 마이크로 서비스로 구현하고 싶었기 떄문에 어려운 작업을 다시 해야 했다.
(5개월짜리 프로젝트가 10개월로 길어졌다.)


그러나 기존의 RDBMS는 Scale Out 하게 확장이 불가능하고, 컨테이너 위에 올리기 어렵다.
이에 물리적인 서비스에 올리기는 힘들겠다는 생각을 하게 됨.

그래서 다시 Legacy Service로 돌아갔다
내부적으로는 다 분리가 되었으나, 디비와 서비스를 하나에 다시 넣었다.
(사진)

### DC/OS

(사진-DC/OS)

디비를 매니징 하는 부분을 서비스로 만드는 아이디어

### 서비스가 많아지면 -> 복잡도가 높아지는데...
공통적으로 사용되어야 할 것이 늘어날 것이고,
이 경우 하나의 빨간 점에서 장애가 발생하면 다른 곳도 장애 발생
따라서 마이크로 서비스가 늘어난다면, re Architecturing을 해줘야 할 것이라고 생각한다.
즉 빨간 점을 다시 다른 서비스로 만들어주는 것


# 컨테이너 기반 Deep Learning 사례 By 신종민 이사(HPE KOREA)
---

# DC/OS 기반 SK HUNIX 차세대 업무 환경 By 서동호 책임(SK HYNIX)
---

### 누구나 가지고 있는 공룡: Legacy
1. 서비스 제공자 중심의 시스템 설계
사용자 중심이 아닌 서비스 제공자 중심의 설계

2. 단기간에 찍어낸 Monolithic 구조
낮은 서버 기동률, 대규모의 traffic 발생 및 분산처리의 어려움

3. DB 중심의 서비스 구조, 복잡한 인터페이스
모든 속도가 DB Query 속도에 종속적

4. 수동적인 시스템
실제 시스템을 찾아가고, 조회, 결과 기다림, 그 결과를 이메일로..

### 차세대 서비스 방향성 설정
1. 서비스 제공자 중심 -> **사용자 중심의 정보, 업무 환경 통합**
: My Work Place
2. Monolithic 구조 -> **Scale-Out을 고려한 Architecture**
: MSQ, Cloud Ready
3. DB 중심의 서비스 구조 -> **Cache, Queue 도입 서비스**
4. 수동적 시스템 -> **능동적 시스템**



# DEVOPS With DC/OS By 최명규 DEVOPS(비바리퍼블리카(TOSS))
---
