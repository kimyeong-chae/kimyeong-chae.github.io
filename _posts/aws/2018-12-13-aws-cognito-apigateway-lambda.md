---
layout: post
title:  "AWS Lambda + Api Gateway + Cognito OAuth2 설정해보기(1)"
date:   2018-12-13 21:30:21 +0900
categories: aws
author : yckim
---


요즘 핫한 서버리스를 구현하기 위해 **Lambda + API Gateway**를 많이 사용하는데 여기에 **Cognito**를 더해 보안이슈까지 해결해보자



### Cognito 설정

##### &nbsp;&nbsp;&nbsp;&nbsp; AWS 콘솔 접속 후 Cognito 서비스 호면에서 *사용자 풀 관리*  &nbsp;
![cognito-1](/img/post/20181213/cognito-1.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; *사용자 풀 생성* &nbsp; 클릭
![cognito-2](/img/post/20181213/cognito-2.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 풀 이름 입력하고 *기본값 검토* &nbsp;
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 다음 화면에서 *풀 생성*
![cognito-3](/img/post/20181213/cognito-3.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 일반설정 > 앱 클라이언트 > 앱 클라이언트 추가
![cognito-4](/img/post/20181213/cognito-4.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; *앱 클라이언트 이름* 입력 후 *앱 클라이언트 생성*
![cognito-5](/img/post/20181213/cognito-5.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 앱 통합 > 도메인 이름 > 도메인 이름 입력, 가용성 확인 후 저장
![cognito-6](/img/post/20181213/cognito-6.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 앱 통합 > 리소스 서버 > *리소스 서버 추가* 선택 후 *이름*, *식별자*를 입력해주세요
##### &nbsp;&nbsp;&nbsp;&nbsp; 여기서 입력한 *식별자*와 *범위 이름*이 토큰 발급시 사용되게 됩니다
![cognito-7](/img/post/20181213/cognito-7.png )

##### &nbsp;&nbsp;&nbsp;&nbsp; 앱 통합 > 앱 클라이언트 설정 > *Cognito User Pool, Client credentials, 허용된 사용자 지점 범위*  &nbsp; 체크 후 저장
![cognito-8](/img/post/20181213/cognito-8.png )

### 여기까지 따라오셨으면 Cognito 설정은 끝났습니다 다음 글로 ㄱㄱ
