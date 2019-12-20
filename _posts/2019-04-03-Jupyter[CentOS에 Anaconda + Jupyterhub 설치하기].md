---

title : "CentOS에 Anaconda + Jupyterhub 설치하기"
date : 2019-04-03 10:00:00 + 0000
tags: Anaconda, Jupyterhub
category: Tool

---

# Intro
이번 포스트에서는 CentOS에 Anaconda와 Jupyterhub를 설치하는 방법을 설명하였다.

***

# 1. 사전 작업: jupyter user 계정 생성
여기서는 Jupyterhub를 운영을 편리하게 하기 위해서 jupyter 계정을 별도로 생성한다. Jupyterhub를 구축하고 나면 userdata 디렉토리를 설정하게 되는데, 이때 jupyter 계정의 home 디렉토리의 하위 디렉토리로 설정할 것이다. 먼저 jupyter user 계정을 생성하자.

```bash
useradd jupyter # jupyter user 생성
passwd jupyter  # jupyter user 패스워드 설정
```

***

# 2. Anaconda 설치

## 2-1. Anaconda 설치 파일 다운로드

먼저 jupyter 계정의 home 디렉토리 경로에 anaconda 디렉토리를 생성하고, 해당 경로에 ananconda를 설치하도록 한다.

Anaconda 설치 파일을 다운로드 해야 하는데, 최신 버전은 [여기서](https://repo.continuum.io/archive/) 확인할 수 있다. Ananconda 설치 파일 다운로드 링크 주소를 복사해서 다음 명령으로 다운로드 하면 된다.

```
# anaconda 디렉토리 생성
mkdir /home/jupyter/anaconda
cd /home/jupyter/anaconda

# anaconda 설치 파일 다운로그
wget {링크 주소}
ex) wget  https://repo.continuum.io/archive/Anaconda2-5.3.1-Linux-x86_64.sh
```

## 2-2. Anaconda 설치

먼저 다운로드한 설치 파일을 실행 가능하도록 권한을 변경해줘야 한다. 그리고 설치를 진행하면 된다. 이때, 매개변수를 명령어에 추가하여 특정 디렉토리에 설치가 가능하다. 여기서는 /home/jupyter/anaconda/ 경로에 설치했다.

```
# 설치 가능하도록 권한 변경
chmod +x {설치 파일}
ex) chmod +x Anaconda2-5.3.1-Linux-x86_64.sh

# anaconda 설치
 ./Anaconda2-5.3.1-Linux-x86_64.sh

# 특정 디렉토리에 설치하고 싶으면, 다음과 같이 설치 명령어를 입력하면 된다.
./{설치 파일} -b -p {경로} -f
ex) ./Anaconda2-5.3.1-Linux-x86_64.sh -b -p /home/jupyter/anaconda -f
```

마지막으로 anaconda 사용을 위해 환경 변수를 설정해줘야 한다. /etc/profile 파일을 열어서 해당 path를 추가하자.

```
vi /etc/profile

# 아래의 PATH 추가
export PATH=$PATH:/home/jupyter/anaconda/bin
```

![JupyterSeries1-(1)](/assets/images/2019-04-13-JupyterSeries1/1.png){: width="900" height="700"}

그리고 설정한 환경 변수 변경을 적용해주면 anaconda 설치가 완료된다.

```
# 환경 변수 적용
source /etc/profile
```

***

# 3. Jupytehub 설치
Jupyterhub를 독립적인 환경에서 구축하기 위해서, conda 가상환경을 만들고 그 위에 Jupyterhub를 설치하는 방법을 설명한다(conda 가상환경 위에 Jupyterhub를 설치하는 것 외에는 기존의 Jupyterhub 설치 방법과 동일하다).

## 3-1. Python3 가상환경 생성
conda 가상환경을 생성하고 실행 및 중지하는 방법을 알아보자.

```
# 가상환경 생성하기
conda create -n {가상환경 명} python={파이썬 버전} anaconda
ex) conda create -n jupyterhub python=3.6 anaconda

# 가상환경 실행하기
source activate {가상환경 명}
ex) source activate jupyterhub

# 가상환경 나가기
source deactivate
```

생성된 가상환경의 목록은 아래의 명령어로 조회할 수 있다. Jupyterhub 가상환경이 생성된 것을 확인해보자.

```
# 가상환경 리스트 확인
conda info --envs
```

## 3-2. Npm, Node js, Proxy 설치
Jupyterhub를 설치하기 위해서는 npm, node js, configurable http proxy 설치가 필요하다.
아래의 명령어를 차례로 입력하여 설치를 진행하면 된다.

```
# 설치
curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -
sudo yum install nodejs

# 버전 확인
node --version
npm --version

# configurable http proxy 설치
sudo npm install -g configurable-http-proxy
```

## 3-3. Jupyterhub 설치 및 시작
Jupyterhub를 설치하는 명령은 간단하다.

```
# 먼저 Jupyterhub 가상환경에 들어가서
source activate jupyterhub

# pip로 설치해주면 끝!
pip install jupyterhub

# JUpyterhub 설치 확인
jupyterhub -h
```

이제 거의 끝났다. Jupyterhub 설정을 위해 설정 파일을 생성하고, Jupyterhub를 시작해보자.

```
# Jupyterhub 설정 파일 생성
cd /home/jupyter/
jupyterhub --generate-config -f /home/jupyter/jupyterhub/jupyterhub_config.py <--- config 파일을 원하는 경로에 생성할 수 있다.

# Jupyterhub 실행
jupyterhub
```

http://localhost:8000 주소로 접속하면 Jupyterhub에 로그인할 수 있다.

![JupyterSeries1-(2)](/assets/images/2019-04-13-JupyterSeries1/2.png){: width="900" height="700"}

**PAM 로그인**
참고로 Jupyterhub는 기본적으로는 PAM(Pluggable Authentication Module) 로그인을 방법을 사용한다. 로그인 방법에 대해서는 추후 자세히 설명하도록 하고, Jupyterhub를 생성한 계정으로 로그인하면 된다.
