---
title: OracleDB Cold Backup
date: 2018-09-22 18:43:29
categories: [work]
tags: [work, Oracle, Backup]
---

## 백업 대상

1. Data File
1. 실제 데이터가 저장되어 있는 파일
1. 현재 사용중인 Data File을 확인 후, 자주 백업 받아야 함
1. 조회방법
```
SELECT name, status FROM v$datafile ;

SELECT a.file#, a.name, b.name tsname, a.status
    FROM v$datafile a, v$tablespace b
    WHERE a.ts# = b.ts# ;
```
## ontrol File
1. DB를 운영하는데 중요한 내용이 들어있는 파일
1. 현재 사용중인 Control File만 쓸 수 있음, 과거에 썼던 파일은 백업 받아도 소용 없음
1. 조회방법
```
SELECT name FROM v$controlfile ;
```
## Redo Log File
1. 데이터에 변경이 일어난 내용을 복구에 사용하기 위해 저장하고 있는 파일
1. 조회방법
```
SELECT a.group#, a.member, b.bytes/1024/1024 MB, b.archived, b.status
    FROM v$logfile a, v$log b
    WHERE a.group# = b.group#
    ORDER BY 1, 2 ;
```
## Parameter File
1. 오라클 서버를 운영하는데 필요한 각종 설정 정보를 저장 하고 있는 파일
1. 이 파일이 손실되면 오라클 서버가 시작되지 않음
1. 필수 백업 파일은 아니지만 백업 받아 두는 것이 훨씬 유용
1. 위치는 $ORACLE_HOME/dbs
1. pfile은 initSID.ora / spfile은 spfileSID.ora
1. 조회방법
```
show parameter spfile ;
show parameters;
```
## Password File
1. 암호파일, sys계정의 암호를 저장하는 일반 파일 
1. 파라미터 파일과 동일한 디렉토리에 저장되어 있음 = $ORACLE_HOME/dbs
1. 이름은 orapwSID
1. 역시 필수 백업 파일은 아니지만 백업을 권장