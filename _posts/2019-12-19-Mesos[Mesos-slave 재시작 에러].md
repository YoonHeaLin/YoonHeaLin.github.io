---

title : "Mesos-slave 재시작 에러"
date : 2019-12-19 10:00:00 + 0000
tags: Mesos
category: Tool

---

### Error

```
[root@rin_gu ~]$ systemctl status mesos-master
● mesos-master.service - Mesos Master
   Loaded: loaded (/usr/lib/systemd/system/mesos-master.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
```

### Solution

에러 로그 확인
```
$ cat /var/log/mesos/mesos-slave.ERROR
```

work 디렉토리 확인
```
$ cat /etc/mesos-slave/work_dir
```

latest 파일 제거
```
$ rm -f /var/lib/mesos/meta/slaves/latest
```

재시작
```
$ systemctl restart mesos-slave
$ systemctl status mesos-slave
```

정상적으로 작동하는 것을 확인할 수 있음

### 참고 사이트
-  https://gist.github.com/lava/bd9b7c90c067ae3298f7daf2df9fd99f

```
E1103 18:30:03.451825 12204 slave.cpp:6302] EXIT with status 1: Failed to perform recovery: Incompatible agent info detected.
    ------------------------------------------------------------
    [...]
    ------------------------------------------------------------
    To remedy this do as follows:
    Step 1: rm -f /path/to/work_dir/meta/slaves/latest
            This ensures agent doesn't recover old live executors.
    Step 2: Restart the agent.
```
