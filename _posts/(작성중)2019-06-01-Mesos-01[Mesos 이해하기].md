---

title : "Mesos 이해하기"
date : 2019-06-01 10:00:00 + 0000
tags: Mesos
category: Tool

---

# Intro

이번 포스트에서는 Cloud Infrastructure 및 Computing Engine들의 자원을 통합적으로 관리 가능한 "자원 관리 프로젝트"인 Mesos를 소개한다.

***

# 1. Mesos 란?

Mesos는 분산 시스템 커널(Distibuted System Kernel)로서, 네트워크로 묶여 있는 여러개의 컴퓨터 자원(CPU, 메모리, 디스크 등)을 묶어서 resource pool로 만들어 마치 하나의 컴퓨터처럼 사용할 수 있게 한다.

***

# 2. Mesos Arichitecture

위의 그림은 Mesos 아키텍처이다.
