---

title : "Docker 설치하기"
date : 2019-06-01 10:00:00 + 0000
tags: Docker
category: Tool

---

# Intro
이번 포스트에서는 CentOS에 Docker를 설치하는 방법을 정리하였다.

***

#  
# 1. Docker 설치하기

```
# yum 패키지 업데이트
yum update

# docker, docker registry 설치
yum -y install docker docker-registry
```

***

#  
# 2. Docker 실행 및 정보 확인

## 2-1. Docker 실행하기

```
# 시스템 부팅 시 docker를 시작하도록 설정
systemctl enable docker.service

# Docker 실행
systemctl start docker.service

# Docker 상태 확인
systemctl status docker.service
```

## 2-2. Docker 명령어 사용하기

Docker 명령어의 기본 형식은 `docker {명령어}`이다.

```
# Docker 버전 확인
docker version

# Docker 실행 환경 확인
docker system info

# Docker 디스크 상태 확인
docker system df

# 그 외 Docker 명령어 살펴보기
docker -help
```

***

# 3. Docker 사용해보기

Docker가 정상적으로 동작하는지 확인하기 위해 컨테이너를 실행해보자.

## 3-1. Docker 컨테이너 실행하기

```
# Docker 컨테이너 실행 명령어
docker run {옵션} {컨테이너 명/ID}
```

docker run 명령어는 컨테이너를 생성하고 실행시키는 명령어다. 이때 로컬에 이미지가 있는지 학인하고, 없는 경우 docker hub에서 `pull`을 먼저 진행하고 컨테이너는 생성한다.

## 3-2. Hello, world!

```
docker run hello-world
```
hello-world 컨테이너가 실행되면 다음과 같이 메세지가 출력된다.

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
```

## 3-3. Nginx

이번에는 Nginx 웹서버를 docker로 설치해보자.

```
# Nginx 이미지 다운로드
docker pull nginx

# 다운로드한 이미지 확인
docker images

# Nginx 컨테이너 실행
docker run --name nginx-webserver -d -p 80:80 nginx
```

`docker run` 명령어에서 자주 쓰이는 옵션을 살펴보자.
- --name: 컨테이너의 이름을 설정한다.
- -d: 컨테이너를 백그라운드에서 실행시킨다.
- -p: 호스트 포트와 컨테이너 내부의 포트를 매핑한다(형식: -p {host 포트}:{컨테이너 포트}).

실행중인 docker 컨테이너를 확인하고 싶을 때는 `docker ps` 명령어를 사용하면 된다.

```
# 실행중인 컨테이너 확인
docker ps

# 컨테이너 상태 확인
docker container stats
```

마지막으로 Nginx 웹 브라우저에서 접속해보자. http://localhost:80으로 접속하면 된다.

![DockerSeries2-(1)](/assets/images/2019-06-01-DockerSeries2/1.png){: width="900" height="700"}

***

# 참고 사이트
- https://niceman.tistory.com/36
- https://futurecreator.github.io/2018/11/16/docker-container-basics/
- http://pyrasis.com/Docker/Docker-HOWTO
