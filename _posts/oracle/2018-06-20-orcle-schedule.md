---
layout: post
title:  "오라클 스케줄러 등록"
date:   2018-06-20 17:45:21 +0900
categories: oracle
author : yckim
---

오라클 스케줄 등록하기

##### 1. 권한 부여
```
grant create any job to 유저명;
```

##### 2. 오라클 job 등록
```
begin
dbms_scheduler.create_job(                                   -- 신규 JOB을 생성
job_name => 'job명' ,                           -- dbms_scheduler 내에서 사용될 job 이름지정
job_type => 'plsql_block' ,                                -- 5번줄에 적은 프로그램의 타입을 적음
job_action => 'begin 프로시저명; end;' ,            -- 실제 실행될 프로그램을 적는 부분
start_date => systimestamp ,                             -- 해당 job 이 처음 시작될 시간을 지정
repeat_interval => 'freq=daily; interval=1' );        -- 반복할 주기를 지정
end;
```

##### 3. 오라클 스케쥴 실행
```
exec dbms_scheduler.enable('job명') ;
exec dbms_scheduler.run_job('job명') ;
```
