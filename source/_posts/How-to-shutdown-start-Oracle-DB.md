---
title: How to shutdown/start Oracle DB
date: 2018-10-27 10:12:35
tags:
---


## Oracle 서버 정지/재가동
1. 먼저 접속된 유저를 끊는다(리스너 종료)
```
$lsnrctl stop
```

1. sysdba 권한으로 접속
```
$sqlplus "/as sysdba"
```

1. Oracle 종료
```
SQL>shutdown
SQL>shutdown abort
SQL>shutdown immediate
```
    * 추천 방법 : shutdown immediate한후 종료가 안될시 새창을 띠워서 shutdown abort 시킴


1. 오라클 재가동
```
SQL>startup
```

1. 리스너 시작
```
$lsnrctl start
```

### 8i일경우

```
$sqlplus /nolog 
SQL>connect / as sysdba 
SQL>shutdown immediate; 
SQL>startup
```