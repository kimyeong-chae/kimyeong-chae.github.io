---
layout: post
title:  "ora-31655 : no data or metadata objects selected for job"
date:   2018-03-05 15:00:21 +0900
categories: oracle
author : yckim
---

expdp 후 impdp 중 오류 발생

```
ora-31655 : no data or metadata objects selected for job
ora-39154 : objects from foreign schemas have been removed
```

일반적으로 remap_schema 파라미터가 잘못되서 발생하는 에러라고 하는데

나는 기존에도 똑같이 import를 했었음.

구글링을 해보니 import 하려는 user에 imp_full_database가 없을 경우에도 같은 에러 발생

위의 권한 주고 다시 import 해보니 성공.

정리.

##### 1. 위의 오류 발생
##### 2. 명령어의 오류가 아니라고 생각 될 경우 user에 imp_full_database 권한 있는지 확인
