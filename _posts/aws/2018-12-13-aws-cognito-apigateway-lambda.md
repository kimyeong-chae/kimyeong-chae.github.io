---
layout: post
title:  "AWS Lambda + ApiGateway + Cognito 설정해보기"
date:   2018-12-13 21:30:21 +0900
categories: aws
author : yckim
---


요즘 핫한 서버리스를 구현하기 위해 **Lambda + API Gateway**를 많이 사용하는데 여기에 **Cognito**를 더해 보안이슈까지 해결해보자

### Cognito 설정

##### &nbsp;&nbsp;&nbsp;&nbsp; 1. AWS 콘솔 접속 후 Cognito 서비스 호면에서 *사용자 풀 관리*  &nbsp; 클릭
![cognito-1](/img/post/20181213/cognito-1.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 2. *사용자 풀 생성* &nbsp; 클릭
![cognito-2](/img/post/20181213/cognito-2.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 3. 풀 이름 입력하고 *기본값 검토* &nbsp;클릭
![cognito-3](/img/post/20181213/cognito-3.png )
