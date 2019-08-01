---
title: Oracle 통계정보 조회및 통계 갱신
date: 2018-10-30 10:34:45
tags:
---


-- 해당 스키마에 해당하는 테이블과 테이블 스페이스 조회
SELECT OWNER, TABLE_NAME, TABLESPACE_NAME FROM DBA_TABLES WHERE OWNER = '스키마명';

-- 해당 스키마에 해당하는 테이블의 통계정보 조회
SELECT TABLE_NAME, NUM_ROWS, CHAIN_CNT, BLOCKS, EMPTY_BLOCKS, AVG_SPACE, AVG_ROW_LEN FROM DBA_TABLES WHERE OWNER = '스키마명';

-- 해당 스키마에 해당하는 인덱스의 통계정보 조회
SELECT TABLE_NAME, INDEX_NAME, STATUS, NUM_ROWS, LEAF_BLOCKS, BLEVEL FROM DBA_INDEXES WHERE OWNER = '스키마명';

-- 테이블의 통계정보 갱신
EXEC DBMS_STATS.GATHER_TABLE_STATS('스키마명', '테이블명');

-- 스키마안의 모든 세그먼트에 대한 통계정보 갱신
EXEC DBMS_STATS.GATHER_SCHEMA_STATS('스키마명');

-- DBMS_STATS 패키지로 갱신되지 않는 테이블 통계 정보 갱신
ANALYZE TABLE 스키마명.테이블명 COMPUTE STATISTICS;
​
-- DBMS_STATS 패키지로 갱신되지 않는 테이블 통계 정보 갱신(쿼리 생성)
SELECT 'ANALYZE TABLE 스키마명.' || TABLE_NAME || ' COMPUTE STATISTICS;' FROM DBA_TABLES WHERE OWNER = '스키마명';

-- DBMS_STATS 패키지로 갱신되지 않는 인덱스 통계정보 갱신
ANALYZE INDEX 스키마명.인덱스명 VALIDATE STRUCTURE;
SELECT NAME, BLOCKS, LF_ROWS, DEL_LF_ROWS FROM INDEX_STATS;
​
-- DBMS_STATS 패키지로 갱신되지 않는 인덱스 통계정보 갱신(쿼리 생성)
SELECT 'ANALYZE INDEX 스키마명.' || INDEX_NAME || ' VALIDATE STRUCTURE;' FROM DBA_INDEXES WHERE OWNER = '스키마명';
[출처] [오라클] 통계정보 조회 및 통계 갱신|작성자 그늘



출처: http://calsifer.tistory.com/245 [Maybe...]