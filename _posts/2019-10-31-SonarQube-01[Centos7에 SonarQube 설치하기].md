---

title : "Centos7에 SonarQube 설치하기"
date : 2019-10-31 10:00:00 + 0000
tags: SonarQube
category: TestAutomation

---

# Intro

이번 포스트에서는 Centos7에 정적분석 도구 SonarQube를 설치하는 방법을 정리하였다.

***

# 1. 사전 준비

## 1-1. 환경 구성

SonarQube 최신 버전에서 JAVA와 PostgreSQL 호환을 위해서는 버전을 맞춰주는 것이 매우 중요하다.

|환경|요구 사항|설치 버전|
|------|---|---|
|SonarQube|-|7.9.1|
|JAVA|11|11.0.4|
|PostgreSQL|10/9.3-9.6|10|

## 1-2. ElasticSearch 사용을 위한 설정(root 권한으로 수행)
```
$ sysctl -w vm.max_map_count=262144
$ sysctl -w fs.file-max=65536
$ ulimit -n 65536
$ ulimit -u 4096
```

- 영구적으로 설정하는 방법(sysctl)
```
$ vi /etc/sysctl.conf

아래 내용 추가
vm.max_map_count=262144
fs.file-max=65536

확인
$ sysctl -p
```

- 영구적으로 설정하는 방법(ulmit)
```
$ vi /etc/security/limits.conf

아래 내용 추가
*               soft    nofile          65536
*               hard    nofile          65536

확인
$ ulimit -a
$ ulimit -aH
```


## 1-3. Sonarqube 계정 생성
```
$ adduser sonarqube
$ passwd sonarqube
```

***

# 2. JAVA JDK 11 설치

## 2-1. 이미 설치된 JAVA가 있는 경우, 삭제하는 방법

```
# 설치된 자바 확인
$ rpm -qa | grep jdk

# 설치된 자바 삭제
$ yum -y remove java-x
```

## 2-2. JAVA JDK 11 설치

```
# Open JDK 설치
$ yum list java*jdk-devel
$ yum install -y java-11-openjdk-devel.x86_64

# JAVA 버전 확인
$ java -version

# JAVA_HOME 환경 변수 설정
$ which java
$ readlink -f /usr/bin/javac
$ vi /etc/profile

아래 내용 입력
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.4.11-0.el7_6.x86_64

$ source /etc/profile

# 확인
$ echo $JAVA_HOME
```

***

# 3. PostgreSQL 설치

## 3-1. PostgreSQL10 설치

```
# PostgreSQL repository 설치
$ rpm -Uvh https://yum.postgresql.org/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm

# PostgresQL 설치
$ yum install postgresql10-server postgresql10

# PostgreSQL DB 초기화
$ /usr/pgsql-10/bin/postgresql-10-setup initdb

# PostgreSQL 실행
$ systemctl start postgresql-10.service
$ systemctl enable postgresql-10.service

# postgre 계정 비밀번호 변경
$ su - postgres -c "psql"
psql (10.0)
Type "help" for help.

postgres=# \password postgres
```

## 3-2. PostgreSQL 사용자, 데이터베이스 생성
```
postgres=# create user {계정} password '{패스워드}' CreateDB Replication Superuser Createrole;
postgres=# create database {데이터베이스 명} owner={계정};
postgres=# grant all privileges on database {데이터베이스 명} to {계정};
```

## 3-3. PostgreSQL10 외부 접속 허용

먼저 postgresql의 설정 파일인 postgresql.conf 파일을 수정한다.
```
$ vi /var/lib/pgsql/10/data/postgresql.conf

아래 내용 수정
listen_addresses = '*'
```

다음으로 postgresql의 인증시스템 관련 정보 파일인 pg_hba.conf 파일을 수정한다.
```
$ vi /var/lib/pgsql/10/data/pg_hba.conf

아래 내용 추가
# TYPE    DATABASE        USER        ADDRESS        METHOD
host      all             all         0.0.0.0/0      md5
```
Method md5는 패스워드를 md5로 암호화해서 전송하는 것을 의미한다.

## 3-4. PostgreSQL 재시작

설정이 완료되면 PostgreSQL을 재시작해준다.
```
$ systemctl restart postgresql-10.service
$ systemctl status postgresql-10.service
```

아래와 같이 접속이 되는 것을 확인 할 수 있다.
```
$ psql --username=sonar --host={PostgreSQL Server IP} --port={PostgreSQL PORT}
Password for user sonar:
psql (10.10)
Type "help" for help.

sonar=#
```


***

# 4. SonarQube 설치

## 4-1. SonarQube 다운로드
```
$ wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.9.1.zip
$ unzip sonarqube-7.9.1.zip
$ mv sonarqube-7.9.1 /opt/sonarqube
```

## 4-2. SonarQube 설정
```
$ vi /opt/sonarqube/conf/sonar.properties

아래 내용 수정
sonar.jdbc.username={PostgreSQL 계정}
sonar.jdbc.password={PostgreSQL 패스워드}
sonar.jdbc.url=jdbc:postgresql://{PostgreSQL Server IP}:{PostgreSQL PORT}/{데이터베이스 명}

sonar.web.host={SonarQube Server IP}
sonar.web.port={SonarQube PORT}
```

## 4-3. SonarQube 폴더 권한 설정
```
$ setfacl -R -m m::rwx /opt/sonarqube
$ setfacl -R -m u:sonarqube:rwx /opt/sonarqube
$ setfacl -R -m default:u:sonarqube:rwx /opt/sonarqube
```

## 4-4. SonarQube 실행
```
elasticsearch가 함께 실행되므로, sonarqube 계정으로 실행해야 한다
$ su - sonarqube
$ /opt/sonarqube/bin/linux-x86-64/sonar.sh start
```

## 4-5. SonarQube 접속

- 주소: http://{SonarQube Server IP}:{SonarQube PORT}
- 계정: admin
- 패스워드: admin

![SonarQube1](/assets/images/2019-10-31-Centos7에-SonarQube-설치하기/1.PNG){: width="900" height="700"}

***

# 5. SonarQube 백업 및 복원

## 5-1. SonarQube 백업
```
SonarQube 중지
$ /opt/sonarqube/bin/linux-x86-64/sonar.sh stop

데이터 베이스 백업
$ pg_dumpall -c -U postgres > {dump 파일명}.sql

SonarQube 디렉토리 압축
$ zip -r sonarqube.zip /opt/sonarqube
```

## 5-2. SonarQube 복원

복원하려는 서버에서 진행하면 된다.
```
데이터 베이스 복원
$ cat {dump 파일명}.sql | psql -U postgres

SonarQube 디렉토리 복원
$ unzip sonarqube.zip

SonarQube 시작
$ /opt/sonarqube/bin/linux-x86-64/sonar.sh start
```

***

# 참고 사이트
- https://xshine.tistory.com/308
- https://futurecreator.github.io/2018/11/16/docker-container-basics/
- http://pyrasis.com/Docker/Docker-HOWTO
- http://www.scmgalaxy.com/tutorials/sonarqube-upgrade-backup-and-restore-process/
