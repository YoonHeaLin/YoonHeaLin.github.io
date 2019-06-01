---

title : "접근 제어 목록(ACL; Access Control List) 설정하기"
date : 2019-03-26 10:00:00 + 0000
tags: Linux, ACL
category: Linux

---

# Intro
이번 포스트에서는 접근 제어 목록(ACL; Access Control List)에 대하여 정리하였다.

***

# ACL이란?

리눅스에서는 파일이나 디렉토리의 권한을 관리할 때 소유자(owner), 그룹(group), 다른 사용자(other)라는 세 가지 역할에 따라 접근 권한을 부여할 수 있고, 이 작업은 chmod 명령어를 통해 수행한다.

그런데 이러한 세 가지 역할에 따라 접근 권한을 관리하는 데는 여러 가지 제한이 있다. 일례로, 기본 소유자, 그룹 외에 추가적으로 특정 사용자, 그룹에게 디렉토리 권한을 주는 것이 불가능하다.

이러한 문제를 해결하기 위해 리눅스 커널과 파일 시스템에 접근 제어 목록(ACL; Access Control List)이 구현되었다.


# ACL 사용 방법

## 1. ACL 확인

getfacl 명령어로 파일이나 디렉토리에 설정된 ACL을 확인할 수 있다.

```
# getfacl <path>
예) getfacl /data/test
```

위의 예시로 확인해보면 /data/test의 ACL은 아래와 같이 설정되어있다.

## 2. ACL 추가/변경

-m 옵션을 사용하면 파일이나 디렉토리의 ACL을 추가 또는 변경할 수 있다. 아래와 같은 형식으로 설정한다.

```
# setfacl <option> <perm> <path>
예) setfacl -m u:jupyterhub:rwx /data/test
예) setfacl -m g:jupyterhub-users:rwx /data/test
```

위의 예시는 /data/test에 사용자 권한으로 jupyterhub, 그룹 권한으로 jupyterhub-users를 추가한다.
설정 후 getfacl로 해당 경로의 권한을 확인해보면, 아래와 같이 두 권한이 추가된 것을 볼 수 있다.


## 3. ACL Default 설정

그런데 아무리 기존 파일과 디렉토리의 권한을 바꿔줘도 새로 만든 파일의 권한은 소유자, 그룹, other만 기본으로 지정된다면, 매번 setfacl 명령어로 설정해주어야 한다는 문제가 있다.

예를 들어 healin23 계정으로 /data/test 디렉토리 아래 test.txt 파일을 만들고 getfacl로 권한을 확인해보면, 다음과 같이 파일을 생성한 유저(healin23)로 소유자, 그룹, other가 기본으로 설정되는 것을 볼 수 있다.

이러한 문제를 해결하는 방법이 defacult 설정이다. 디렉토리에만 설정이 가능하고, 디렉토리 내에 새로 생성되는 파일은 디렉토리의 default 권한을 상속받는다.

```
# setfacl -m default:<perm> <path>
예) setfacl -m default:g:jupyterhub-users:rwx /data/test
```

위의 예시는 /data/test 디렉토리의 권한과 같이, 해당 디렉토리 아래 파일을 생성해도 jupyterhub-user 그룹에 rwx 권한이 부여되도록 한다.
새로 파일을 생성하여 getfacl로 확인해보면 다음과 같다.
