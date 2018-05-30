---
layout: post
title:  "Nginx SSL 설정"
date:   2018-05-30 09:11:21 +0900
categories: linux
author : yckim
---

#### Nginx 설치

Nginx 설치는 **yum** 을 이용해서 설치함

설치하고나면

<code>
$ cd /etc/nginx/
</code>


경로에서 Nginx 설정파일들을 확인 할 수 있다

--------------

#### Nginx SSL 설정

기존에 apache2.2에서 쓰던 ssl인증서를 그대로 사용함

먼저 Nginx 설정 파일

```
server {
    listen       80;
    server_name  www.example.com;

    location / {

    }
}


server {
    listen       443;
    server_name  www.example.com

    ssl                  on;
    ssl_certificate      /etc/nginx/ssl/www.example.com.chained.crt;
    ssl_certificate_key  /etc/nginx/ssl/www.example.com.key;
    ssl_session_timeout  5m;
    ssl_protocols  TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers   'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
    location ~ /\.ht {

    }
}
```

기존에 파일들은 총 3개다

```
CA인증서

SSL인증서

키
```

아파치에서는 3개 파일 전부 설정할 수 있는데 Nginx에서는 인증서 파일 설정하는 부분이 2개밖에 없음

그래서 **SSL인증서와 CA인증서를 합쳐서 설정해야 함**

<code>
  $ cat SSL인증서경로 CA인증서경로 > 합친파일명
</code>

합쳐준 후 위에

ssl_certificate			합친파일경로
ssl_certificate_key		키파일경로

설정해주면 끝!


---

#### 개인키 비밀번호 설정

위처럼 설정하고 Nginx를 시작했을 때 비밀번호 떄문에 시작이 되지 않았었음

구글링 결과

<code>
  $ cp 개인키.key 개인키복사본파일명.key.secure
</code>


<code>
  $ openssl rsa -in 개인키복사본파일명.key.secure -out 개인키.key
</code>

패스워드 입력하면 끝!
