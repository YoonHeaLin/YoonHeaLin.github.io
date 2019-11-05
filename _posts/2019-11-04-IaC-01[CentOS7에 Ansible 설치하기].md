---

title : "Centos7에 Ansible 설치하기"
date : 2019-11-04 10:00:00 + 0000
tags: Ansible
category: IaC

---

# Intro

이번 포스트에서는 Centos7에 Ansible를 설치하는 방법을 정리하였다.

***

# 1. 개념

## 1-1. Ansible 이란 (작성중)


## 1-2. (작성중)

***

# 2. Asible 설치

## 2-1. pip 설치
```
$ curl -fsSL https://bootstrap.pypa.io/get-pip.py | python2
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Collecting pip
  Downloading https://files.pythonhosted.org/packages/00/b6/9cfa56b4081ad13874b0c6f96af8ce16cfbc1cb06bedf8e9164ce5551ec1/pip-19.3.1-py2.py3-none-any.whl (1.4MB)
     |████████████████████████████████| 1.4MB 853kB/s
Collecting wheel
  Downloading https://files.pythonhosted.org/packages/00/83/b4a77d044e78ad1a45610eb88f745be2fd2c6d658f9798a15e384b7d57c9/wheel-0.33.6-py2.py3-none-any.whl
Installing collected packages: pip, wheel
Successfully installed pip-19.3.1 wheel-0.33.6
```

## 2-2. Ansible 설치
```
$ pip2 install ansible
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Collecting ansible
  Downloading https://files.pythonhosted.org/packages/59/3a/5b8aeca9b0b68e7a02fdfd7260f265be3b0605839d7367501aba4bcb2e14/ansible-2.9.0.tar.gz (14.1MB)
     |████████████████████████████████| 14.1MB 118kB/s

...

Installing collected packages: ansible
Successfully installed ansible-2.9.0
```

## 2-3. Ansible 최신 버전으로 업데이트
```
$ pip2 install -U ansible

구체적으로 설치할 버전을 지정하고 싶을 경우
$ pip2 install -U ansible=={버전}
```

## 2-4. Ansible 동작 확인
```
$ ansible localhost -m ping
[WARNING]: No inventory was parsed, only implicit localhost is available

localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}

```

***

***

# 참고 사이트
- https://zigispace.net/920
