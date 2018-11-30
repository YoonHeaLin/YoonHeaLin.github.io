---

title : "우분투(Ubuntu) 16.04에 아나콘다(Anaconda) 설치하기 / 주피터 노트북(Jupyter Notebook) 시작하기"
date : 2018-11-30 10:00:00 + 0000
tags: Python
category: Python

---

# Intro
아나콘다(Anaconda)란 파이썬(Python) 기반의 데이터 분석에 필요한 오픈소스들을 모아 놓은 데이터 과학(개발) 플랫폼이다. 이번 포스트에서는 우분투(Ubuntu) 16.04에 아나콘다를 설치하는 방법을 정리하였다.

***

# 아나콘다(Anaconda) 설치

## 1. 아나콘다 설치 파일 다운로드
[https://www.anaconda.com/download/#linux](https://www.anaconda.com/download/#linux)에서 Linux 환경의 설치 파일을 다운로드 한다.


## 2. 아나콘다 설치
설치 파일이 있는 디렉토리로 이동하여 다음의 명령어를 실행한다.

`bash Anaconda3-5.3.1-Linux-x86_64.sh`

다음과 같은 목록에 `Enter` 키와 `yes` 등을 통해 동의하여 설치를 진행한다.
- 라이센스 동의
- 설치 경로(일반적으로 /home/[userid]/anaconda3로 지정)

설치가 완료되면 다음과 같은 화면이 출력된다.
![Anaconda1](/assets/images/2018-11-30-python/1.PNG){: width="640" height="500"}

다음 명령어를 통해 아나콘다를 활성화 시킨다.
`source ~/.bashrc`

아나콘다가 제대로 설치되었는지 확인하기 위해 아래 명령어를 입력한다.
`conda --version`

![Anaconda2](/assets/images/2018-11-30-python/2.PNG){: width="640" height="500"}

# 아나콘다 환경 설정

## 1. 가상 환경
파이썬에서는 가상 환경(virtual environment)을 제공하는데, 가상 환경은 독립된 공간을 만들어주는 기능이다. 가상 환경에서 독립적으로 패키지를 설치하면, 파이썬 스크립트를 실행할 때도 현재 가상 환경에 설치된 패키지를 사용하므로 버전 호환 문제가 발생하지 않는다.

가상환경에 대한 자세한 설명은 [파이썬 가상 환경](https://dojang.io/mod/page/view.php?id=1168)를 참고하면 된다.

## 2. 아나콘다 가상 환경 만들기
아나콘다는 아나콘다 전용 가상 환경을 제공하며, conda를 사용하여 가상 환경을 만들 수 있다.

'pythonPractice'라는 콘다(conda) 가상 환경을 만들어준다. 여기서는 파이선 3.6 버전을 사용하였다.
`conda create -n pythonPractice python=3.6`

중간에 Proceed 질문은 'y'를 입력해주면 된다. 콘다 가상 환경 공간이 만들어지면 다음과 같이 화면에 출력된다.
![Anaconda3](/assets/images/2018-11-30-python/3.PNG){: width="640" height="500"}

콘다 공간에 들어가고 / 나오기 위해서는 각각 아래의 명령어를 입력하면 된다.
`source activate pythonPractice`
`source deactivate`
![Anaconda4](/assets/images/2018-11-30-python/4.PNG){: width="640" height="500"}

추가로 콘다 공간을 지우려면 아래의 명령어를 입력하면 된다.
`conda uninstall [콘다 공간 이름]`

## 3. 주피터 실행하기
주피터를 실행하기 위해 명령창에 다음과 같이 입력한다.
`jupyter notebook --ip=0.0.0.0 --port=8889`

서버에 웹브라우저가 설치되어 있지 않다면, 아래와 같은 에러가 출력될 것이다.
![Anaconda5](/assets/images/2018-11-30-python/5.PNG){: width="640" height="500"}

맨 아래에 출력된 주소를 복사해서 로컬 컴퓨터의 웹브라우저에 접속하면 제대로 동작하는 것을 확인할 수 있다.
![Anaconda6](/assets/images/2018-11-30-python/6.PNG){: width="640" height="500"}

***

# 참고
https://antilibrary.org/1746
http://www.openwith.net/wp-content/uploads/2018/01/%EC%95%84%EB%82%98%EC%BD%98%EB%8B%A4%EC%99%80-%EC%A3%BC%ED%94%BC%ED%84%B0.pdf
https://dojang.io/mod/page/view.php?id=1168
