---

title : "Git-Authentication failed 에러"
date : 2019-12-12 10:00:00 + 0000
tags: TroubleShooting, Git
category: Git

---

### Error

```
remote: HTTP Basic: Access denied
fatal: Authentication failed for ~
```

### Solution
관리자 권한으로 bash 실행

```
$ git config --system --unset credential.helper
$ git config --global --unset credential.helper
```
