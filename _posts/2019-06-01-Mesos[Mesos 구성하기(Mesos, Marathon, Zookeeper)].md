---

title : "Mesos 구성하기(Mesos, Marathon, Zookeeper)"
date : 2019-06-01 10:00:00 + 0000
tags: Mesos, Marathon, Zookeeper
category: Tool

---

# Intro
이번 포스트에서는 CentOS에서 Mesos를 구성하는 방법을 정리하였다.

***

# 1. Mesos Cluster 정보

여기서 구성한 Mesos Cluster 정보는 다음과 같다.

Host | 역할 | 설치 애플리케이션
--- | --- | ---
Mesos01 | Master | Mesos-Master, Zookeeper, Marathon, Docker
Mesos02 | Master | Mesos-Master, Zookeeper, Marathon, Docker
Mesos03 | Master | Mesos-Master, Zookeeper, Marathon, Docker
Mesos04 | Slave | Mesos-Slave, Docker
Mesos05 | Slave | Mesos-Slave, Docker
Mesos06 | Slave | Mesos-Slave, Docker
Mesos07 | Slave | Mesos-Slave, Docker

이제 Mesos Cluster를 구축하기 위해 각 서버에 애플리케이션을 설치하고 설정해보자.

***

# 2. Mesos Cluster 구축 사전 작업

## 2-1. Hostname 등록하기

먼저 모든 서버의 `/etc/hosts` 파일에 hostname을 등록해야 한다. 모든 서버에서 아래와 같이 설정 작업을 하자.

```
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6

# Mesos Cluster
{Server IP}  Mesos01
{Server IP}  Mesos02
{Server IP}  Mesos03
{Server IP}  Mesos04
{Server IP}  Mesos05
{Server IP}  Mesos06
{Server IP}  Mesos07
```

## 2-2. Java 설치

Zookeeper를 사용하기 위해서는 Java가 설치되어 있어야 한다. Zookeeper 사용을 위해서는 Master에만 설치해도 되지만 Java는 다양하게 사용되므로 Slave에도 설치하도록 하자.

모든 서버에서 아래의 명령어를 통해 Java를 설치하자.

```
# Java가 설치되어 있는지 확인
java -version
javac -version

# Java 설치
yum list java*jdk-devel
yum install -y java-1.8.0-openjdk-devel.x86_64
rpm -qa | grep java
```

## 2-3. Docker 설치

모든 서버에서 아래의 명령어를 통해 Docker 설치 및 설정을 진행하자.

```
# yum 패키지 업데이트
yum update

# docker, docker registry 설치
yum -y install docker docker-registry

# 시스템 부팅 시 docker를 시작하도록 설정
systemctl enable docker.service

# Docker 실행
systemctl start docker.service

# Docker 상태 확인
systemctl status docker.service
```

## 2-4. Mesos 저장소 설치

다음으로 모든 서버에 Mesos 저장소를 설치해주어야 한다. 최신 버전은 여기(작성중)에서 확인할 수 있다.
모든 서버에서 아래의 명령어를 수행하여 저장소를 설치하자.

```
rpm -Uvh http://repos.mesosphere.com/el/7/noarch/RPMS/mesosphere-el-repo-7-1.noarch.rpm
```

***

# 3. Mesos Cluster 구축

이제 본격적으로 각 서버에 Mesos를 구성할 것이다. 설치와 설정해야 하는 것이 많으므로 누락되는 것이 없도록 주의해야 한다.

또한 Mesos를 실행하는 순서도 중요하므로, 아래의 순서대로 작업을 수행하는 것을 권장한다.

## 3-1. Mesos01~Mesos03 서버에서 작업(Master)

```
# 1. Mesos 패키지 설치
yum -y install mesos

# 2. Mesos Master 설정
echo {해당 마스터 노드의 IP주소} > /etc/mesos-master/ip

echo {해당 마스터 노드의 IP주소} > /etc/mesos-master/hostname

# 3. Zookeeper 설치
yum -y install mesosphere-zookeeper

# 4. Zookkeper 설정
echo 1 > /var/lib/zookeeper/myid

vi /etc/zookeeper/conf/zoo.cfg --> 아래 내용 추가
server.1={mesos01의 IP 주소}:2888:3888  
server.2={mesos02의 IP 주소}:2888:3888
server.3={mesos03의 IP 주소}:2888:3888

echo 'zk://{mesos01의 IP 주소}:2181,{mesos02의 IP 주소}:2181,{mesos03의 IP 주소}:2181 /mesos' > /etc/mesos/zk

echo 2 > /etc/mesos-master/quorum

# 5. Marathon 설치
yum -y install marathon

# 6. Marathon 설정
sudo mkdir -p /etc/marathon/conf
sudo cp /etc/mesos-master/hostname /etc/marathon/conf/hostname

sudo cp /etc/mesos/zk /etc/marathon/conf/master  

touch /etc/marathon/conf/zk
echo 'zk://{mesos01의 IP 주소}:2181,{mesos02의 IP 주소}:2181,{mesos03의 IP 주소}:2181/marathon' > /etc/marathon/conf/zk

vi /etc/default/marathon --> 아래 내용 추가
MARATHON_MASTER="zk://{mesos01의 IP 주소}:2181,{mesos02의 IP 주소}:2181,{mesos03의 IP 주소}:2181/mesos"
MARATHON_ZK="zk://{mesos01의 IP 주소}:2181,{mesos02의 IP 주소}:2181,{mesos03의 IP 주소}:2181/marathon"
```

## 3-2. Mesos04~Mesos07 서버에서 작업(Slave)

```
# 1. Mesos 패키지 설치
yum -y install mesos

# 2. Mesos Slave 설정
echo {해당 슬레이브 노드의 IP주소} > /etc/mesos-slave/ip

echo {해당 슬레이브 노드의 IP주소} > /etc/mesos-slave/hostname
```

***

# 4. Mesos Cluster 시작

## 4-1. Mesos 서비스 실행(순서대로 하는 것이 중요)

```
# Mesos01 서버에서
systemctl start mesos-master
systemctl start zookeeper
systemctl start marathon

# Mesos02 서버에서
systemctl start mesos-master
systemctl start zookeeper
systemctl start marathon

# Mesos03 서버에서
systemctl start mesos-master
systemctl start zookeeper
systemctl start marathon

# Mesos04~07 서버에서
systemctl start mesos-slave
```

## 4-2. Mesos 서비스 동작 확인

```
# Master 서버에서 mesos-master 서비스 동작 확인
systemctl status mesos-master
systemctl status zookeeper

# Master 서버에서 zookeeper leader/follower 여부 확인
echo srvr | nc localhost 2181

# Slave 서버에서 mesos-slave 서비스 동작 확인
systemctl status mesos-slave
```

## 4-3. 웹 접속

드디어 Mesos 구성이 끝났다. 아래의 웹 페이지에 접속해서 Mesos 동작을 확인할 수 있다.

- Mesos 웹 페이지: http://{Master IP}:5050
- Marathon 웹 페이지: http://{Master IP}:8080
