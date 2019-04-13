---

title : "Jupyter(Notebook, Hub, Lab)에 가상환경 Kernel 추가하기"
date : 2019-03-20 10:00:00 + 0000
tags: Anaconda, Jupyter, Python, R
category: Python

---

# Intro
이번 포스트에서는 Jupyter Notebook, JupyterHub, JupyterLab 등에 가상환경 kernel을 추가하는 방법을 정리하였다. 여기서는 Anaconda 가상환경으로 설명하겠지만, virtualen 가상환경도 동일하게 적용 가능하다.

Jupyter에서 가상환경 kernel을 사용하는 이유는 각 kernel 별로 독립된 환경을 제공하기 위해서이다. 이런 방법으로 R, Tensorflow 등 다양한 개발 환경을 독립적으로 분리하고, Jupyter에서 Kernel로 편리하게 사용할 수 있다.

가상환경 kernel을 Jupyterhub에 추가하기 위해서는 일반적으로 다음과 같은 절차가 필요하다.
- 가상환경 생성
- 가상환경에 개발 환경 구성(R, Tensorflow, Spark 등 가상환경 kernel의 용도에 맞게 환경 구성)
- 가상환경을 Jupyterhub(또는 Jupyter Notebook, Jupyterlab) kernel에 추가

***



## 2. Python3 Kernel 생성

Jupyter Kernel 경로에 새로 등록할 Kernel을 추가해주어야 한다.
```
# Kernel 추가
mkdir /usr/local/share/jupyter/kernels/python3
```

위의 경로에 kernel.json 파일을 생성하고, 아래의 설정을 입력한다.
```
vi /usr/local/share/jupyter/kernels/python3/kernel.json

# 아래 설정 입력(경로에 맞게 적절하게 수정해주어 한다)
{
 "argv": [ "/data/anaconda/envs/python3/bin/python", "-m", "ipykernel",
          "-f", "{connection_file}"],
 "display_name": "Python3",
 "language": "python"
}
```

Jupyter kernel 목록을 확인하면, python3가 추가 된 것을 확인할 수 있다.
```
jupyter kernelspec list
```

***

# Tensorflow Kernel 생성

Jupyterhub에 Tensorflow 가상환경 Kernel을 추가해보자. 위에서 설명한 대로 아래와 같은 순서로 진행될 것이다.
- 가상환경 생성(가상환경 명: Tensorflow, Python 버전: Python3)
- 가상환경에 Tensorflow 설치
- 가상환경을 Jupyterhub에

## 1. 가상환경 생성

```
# 아나콘다 가상환경 생성
conda create -n {가상환경 명} {설치할 패키지}

# 예) 가상환경 이름=Tensorflow + Python 3.6 버전 설치
conda create -n Tensorflow python=3.6

# 가상환경 리스트 확인
conda info --envs
```

## 2.가상환경에 Tensorflow 설치

위에서 생성한 가상환경에 Tensorflow를 설치하기 위해  [https://www.tensorflow.org/install/pip](https://www.tensorflow.org/install/pip)에서 설치할 Tensorflow 패키지를 확인해보자. 설치 환경에 맞게 선택해서 다운로드 링크를 복사해야 한다.

![Tensorflow](/assets/images/2019-03-20-Jupyter/1.PNG){: width="640" height="500"}

Tensorflow 버전에 맞게 다운로드 링크를 확인한 후에, 아래와 같이 가상환경에 Tensorflow 설치를 진행한다.

```
# 가상환경 실행
source activate Tensorflow

# Tensorflow 설치
pip install --ignore-installed --upgrade {packageURL}

예) pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.12.0-cp36-cp36m-linux_x86_64.whl

# 추가 모듈 설치(옵션)
pip install --upgrade numpy scipy wheel cryptography
```

Tensorflow가 잘 설치되었는지 확인하기 위해, Tensorflow 가상환경에서 파이썬을 실행하고 아래 코드로 테스트 해보자.
```
# 파이썬 실행
source activate Tensorflow
python

# Tensorflow 테스트
import tensorflow as tf
hello = tf.constant('hello')
sess = tf.Session()
print(sess.run(hello))
```

## 3. Tensorflow Kernel 생성

위에서 Python Kernel을 추가한 것과 같이, Jupyter Kernel 경로에 새로 등록할 Tensorflow Kernel을 추가해주어야 한다.
```
# Kernel 추가
mkdir /usr/local/share/jupyter/kernels/tensorflow
```

위의 경로에 kernel.json 파일을 생성하고, 아래의 설정을 입력한다.
```
vi /usr/local/share/jupyter/kernels/tensorflow/kernel.json

# 아래 설정 입력(경로에 맞게 적절하게 수정해주어 한다)
{
 "argv": [ "/data/anaconda/envs/tensorflow/bin/python", "-m", "ipykernel",
          "-f", "{connection_file}"],
 "display_name": "tensorflow",
 "language": "python"
}
```

Jupyter kernel 목록을 확인하면, tensorflow가 추가 된 것을 확인할 수 있다.
```
jupyter kernelspec list
```

***



***

# 참고
