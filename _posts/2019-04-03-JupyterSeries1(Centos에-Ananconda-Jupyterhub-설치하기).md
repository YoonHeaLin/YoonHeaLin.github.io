---

title : "CentOS에 Anaconda + Jupyterhub 설치하기"
date : 2019-04-03 10:00:00 + 0000
tags: Anaconda, Jupyterhub
category: Tool

---

# Intro
이번 포스트에서는 CentOS에 Anaconda와 Jupyterhub를 설치하는 방법을 설명하였다.

***

# 사전 작업: jupyter user 계정 생성
jupyter user의 home 디렉토리에서 작업하기 위해서, 먼저 jupyter user 계정을 생성하자.

```bash
useradd jupyter # jupyter user 생성
passwd jupyter  # jupyter user 패스워드 설정
```

# Anaconda 설치
먼저 anaconda 디렉토리를 생성하는 것을 추천한다.
```
mkdir /home/jupyter/anaconda
```

## 1. Anaconda 설치 파일 다운로드
Anaconda 설치 파일을 다운로드 해야 하는데, 최신 버전은 [여기서](https://repo.continuum.io/archive/) 확인할 수 있다.


링크 주소를 복사해서 /home/jupyter/anaconda 경로에서 다음 명령으로 다운로드 하면 된다.
```
wget {링크 주소}
ex) wget  https://repo.continuum.io/archive/Anaconda2-5.3.1-Linux-x86_64.sh
```

## 2. Anaconda 설치
다운로드한 설치 파일을 실행 가능하도록 권한을 변경해주고,
```
chmod +x {설치 파일}
ex) chmod +x Anaconda2-5.3.1-Linux-x86_64.sh
```

설치하면 된다. 이떄, 특정 디렉토리에 설치가 가능하다. 여기서는 jupyter의 home 디렉토리에 설치했다.
```
 ./Anaconda2-5.3.1-Linux-x86_64.sh

# 특정 디렉토리에 설치하고 싶으면, 다음과 같이 설치 명령어를 입력하면 된다.
./{설치 파일} -b -p {경로} -f
ex) ./Anaconda2-5.3.1-Linux-x86_64.sh -b -p /home/jupyter/anaconda -f
```

마지막으로 환경 변수를 설정해줘야 한다. /etc/profile 파일을 열어서,
```
vi /etc/profile
```

아래의 내용을 추가하고,
```
export PATH=$PATH:/home/jupyter/anaconda/bin
```
![JupyterSeries1-(1)](/assets/images/2019-04-13-JupyterSeries1/1.png){: width="640" height="500"}

적용하면 끝난다.
```
source /etc/profile
```

# Jupytehub 설치
Jupyterhub를 독립적인 환경에서 구축하기 위해서, conda 가상환경을 만들고 그 위에 Jupyterhub를 설치하는 방법을 설명한다(conda 가상환경 위에 Jupyterhub를 설치하는 것 외에는 기존의 Jupyterhub 설치 방법과 동일하다).

## 1. Python3 가상환경 생성
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

# 가상환경 리스트 확인
conda info --envs
```

## 2. Npm, Node js, Proxy 설치
Jupyterhub를 설치하기 위해서는 npm, node js, configurable http proxy 설치가 필요하다.

다음 명령으로 npm과 node js를 설치하고,
```
# 설치
curl -sL https://rpm.nodesource.com/setup_10.x | sudo bash -
sudo yum install nodejs

# 버전 확인
node --version
npm --version
```

configurable http proxy도 설치한다.
```
sudo npm install -g configurable-http-proxy
```

## 3. Jupyterhub 설치 및 시작
Jupyterhub를 설치하는 명령은 간단하다.
```
# 먼저 가상환경에 들어가서
source activate Jupyterhub

# 설치해주면 끝!
pip install Jupyterhub

# 설치 확인
jupyterhub -h
```

이제 거의 끝났다. Jupyterhub 설정을 위해 설정 파일을 생성하고, Jupyterhub를 시작해보자.
```
cd /home/jupyter/
jupyterhub --generate-config -f /home/jupyter/jupyterhub/jupyterhub_config.py <--- config 파일을 원하는 경로에 생성할 수 있다.

jupyterhub
```

http://localhost:8000 주소로 접속하면 Jupyterhub에 로그인할 수 있다.
![JupyterSeries1-(2)](/assets/images/2019-04-13-JupyterSeries1/2.png){: width="640" height="500"}

> PAM 로그인
참고로 Jupyterhub는 기본적으로는 PAM(Pluggable Authentication Module) 로그인을 방법을 사용한다.
로그인 방법에 대해서는 추후 자세히 설명하도록 하고,
jupyterhub를 생성한 계정으로 로그인하면 된다.
