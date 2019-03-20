---

title : "Jupyter(Notebook, Hub, Lab)에 가상환경 Kernel 추가하기"
date : 2019-03-20 10:00:00 + 0000
tags: Anaconda, Jupyter, Python, R
category: Python

---

# Intro
이번 포스트에서는 Jupyter Notebook, JupyterHub, JupyterLab 등에 가상환경 kernel을 추가하는 방법을 정리하였다. Anaconda 가상환경으로 설명하겠지만, virtualen 가상환경도 동일하게 적용 가능하다.

Jupyter에서 가상환경 kernel을 사용하는 이유는 각 kernel 별로 독립된 환경을 제공하기 위해서이다. 이런 방법으로 Python, R, Tensorflow 등 다양한 개발 환경을 독립적으로 분리하고, Jupyter에서 Kernel로 편리하게 사용할 수 있다.

***

# Python3 Kernel 생성

## 1. Python3 가상환경 생성

```
# 아나콘다 가상환경 생성
conda create -n {가상환경 명} {설치할 패키지}

# 예) 가상환경 이름=Python3 + Python 3.6 버전 설치
conda create -n Python3 python=3.6
```

## 2. Python3 Kernel 생성

```
# Kernel 추가
mkdir /usr/local/share/jupyter/kernels/python3
```

위의 경로에 kernel.json 파일을 생성하고, 아래의 설정을 입력한다.
```
vi /usr/local/share/jupyter/kernels/python3/kernel.json

# 아래 설정 입력
{
 "argv": [ "/data/anaconda/envs/tensorflow/bin/python", "-m", "ipykernel",
          "-f", "{connection_file}"],
 "display_name": "tensorflow",
 "language": "python"
}
```

Jupyter kernel 목록을 확인하면, Python3가 추가 된 것을 확인할 수 있다.
```
jupyter kernelspec list
```

***

# 참고
