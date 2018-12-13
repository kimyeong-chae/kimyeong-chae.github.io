---
layout: post
title:  "AWS Lambda + Api Gateway + Cognito OAuth2 설정해보기 (2)"
date:   2018-12-14 01:44:21 +0900
categories: aws
author : yckim
---


이전글에서 Cognito 설정을 했고 이번글에서는 **Lambda + Api Gateway** 설정 후 **Cognito**롤 엮는 설정까지 해보겠습니다



### Lambda + API Gateway 설정

#### &nbsp;&nbsp;&nbsp;&nbsp; Lambda > 함수 > 함수 생성
##### &nbsp;&nbsp;&nbsp;&nbsp; 이름 입력하고, 역할이름에서 *1개이상의 템플릿에서 새로운 역할을 생성합니다* 선택하고 *함수 생성*
![lambda-1](/img/post/20181213/lambda-1.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; 자 그러면 밑의 화면이 나올텐데 저기서 API 게이트웨이를 클릭해줍니다
![lambda-1](/img/post/20181213/lambda-2.png )
#### &nbsp;&nbsp;&nbsp;&nbsp;
#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 *새 API 생성* , 보안은 *열기* 로 선택하고 하단의 추가 버튼 클릭하고 상단의 *저장* 을 눌러주세요
#### &nbsp;&nbsp;&nbsp;&nbsp;
![lambda-1](/img/post/20181213/lambda-3.png )
#### &nbsp;&nbsp;&nbsp;&nbsp;
#### &nbsp;&nbsp;&nbsp;&nbsp; 저장을 누르면 API Gateway 이름이랑 상세정보가 나오는데 그중에 *API 엔드포인트* 가 생성한 lambda의 API URL입니다
#### &nbsp;&nbsp;&nbsp;&nbsp;
![lambda-1](/img/post/20181213/lambda-4.png )
#### &nbsp;&nbsp;&nbsp;&nbsp;
#### &nbsp;&nbsp;&nbsp;&nbsp; 이 주소로 Postman 요청을 해보겠습니다
#### &nbsp;&nbsp;&nbsp;&nbsp;
![lambda-1](/img/post/20181213/lambda-5.png )
#### &nbsp;&nbsp;&nbsp;&nbsp; Lambda가 샐행되고 응답이 제대로 오는걸 확인 할 수 있습니다
#### &nbsp;&nbsp;&nbsp;&nbsp; 지금은 *API Gateway* 보안을 *열기* 로 해 놓았기 때문에 누구든 요청할 수 있습니다

#### &nbsp;&nbsp;&nbsp;&nbsp; 그럼 이제 *API Gateway*에 *Cognito* 를 적용해보겠습니다 방금 생성한 *API Gateway* 이름을 클릭해주세요
![lambda-1](/img/post/20181213/lambda-6.png )  

#### &nbsp;&nbsp;&nbsp;&nbsp; API Gateway를 설정할 수 있는 페이지로 넘어오게 됩니다
#### &nbsp;&nbsp;&nbsp;&nbsp; 여기서 *메서드 요청*을 보시면 Auth가 *없음* 으로 되있는 걸 확인할 수 있습니다

#### &nbsp;&nbsp;&nbsp;&nbsp; Cognito 설정을 위해 *권한 부여자*를 생성해야 합니다 좌측의 *권한 부여자* 에서 *새로운 권한 부여자 생성* 을 클릭해주세요  
![lambda-1](/img/post/20181213/lambda-7.png )  


#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 *권한 부여자* 의*이름* 을 입력하고 *유형* 을 *Cognito* 로 선택합니다  

#### &nbsp;&nbsp;&nbsp;&nbsp; 이전 글에서 생성했던 *Cognito 사용자 풀* 이름을 입력합니다
#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 밑에보면 *토큰 원본* 에 *Authorization* 은 Cognito에서 토큰 검증을 위해 필요한 Http Header 항목입니다

#### &nbsp;&nbsp;&nbsp;&nbsp;
#### &nbsp;&nbsp;&nbsp;&nbsp;

#### &nbsp;&nbsp;&nbsp;&nbsp; 다음은 API Gateway 메서드에 방금 생성한 권한 부여자를 설정해보겠습니다
#### &nbsp;&nbsp;&nbsp;&nbsp; 리소스 > ANY 메서드를 선택하고 *메서드 요청* 을 클릭하면 메서드에 대한 승인 정책을 설정할 수 있습니다
#### &nbsp;&nbsp;&nbsp;&nbsp; *승인* 편집 버튼 (좌측에 연필모양) 을 누르시면 방금 생성한 *권한 부여자* 를 선택할 수 있습니다 선택하고 적용해주세요
![lambda-1](/img/post/20181213/lambda-8.png )  

#### &nbsp;&nbsp;&nbsp;&nbsp; 적용하고나면 허용된 OAuth 범위 항목이 생기는데
#### &nbsp;&nbsp;&nbsp;&nbsp; 여기에 Cognito 리소스 서버에 식별자와 범위 이름이
#### &nbsp;&nbsp;&nbsp;&nbsp;
#### &nbsp;&nbsp;&nbsp;&nbsp; 저의 경우엔 yckim-app이 식별자 yckim.read가 범위 이름입니다
![lambda-1](/img/post/20181213/lambda-14.png )  


#### &nbsp;&nbsp;&nbsp;&nbsp; 그러면 바로 Postman에서 다시 요청해보겠습니다
![lambda-1](/img/post/20181213/lambda-5.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; 응답이 정상적으로 옵니다 배포를 안해서 적용이 안되있습니다
#### &nbsp;&nbsp;&nbsp;&nbsp; *작업* 버튼을 눌러 *API 배포* 를 해줍니다 *배포 스테이지* 는 default를 선택해주세요
![lambda-1](/img/post/20181213/lambda-9.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 다시 Postman으로 요청해보겠습니다
![lambda-1](/img/post/20181213/lambda-10.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; *{"message": "Unauthorized"}* 라고 응답이 오네요
#### &nbsp;&nbsp;&nbsp;&nbsp; Cognito가 적용 되었습니다 그럼 Cognito OAuth2 Token 발급 후 발급 받은 토큰으로 다시 요청해보겠습니다

#### &nbsp;&nbsp;&nbsp;&nbsp; 이전 글에서 만들었던 Congito 사용자 풀 관리 화면에서 좌측 사이드에 *앱 통합* 메뉴를 클릭하시면 도메인이 있어요 요걸 복사해줍니다
![lambda-1](/img/post/20181213/lambda-11.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 Postman에서 Authorization 탭으로 이동하고 TYPE을 OAuth2.0을 선택하고 우측에 Get New Access Token 버튼을 눌러주세요
![lambda-1](/img/post/20181213/lambda-13.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; Token Name을 입력하시고
#### &nbsp;&nbsp;&nbsp;&nbsp; Grant Type을 Client Credentials, Access Token URL은 아까 복사한 도메인을 붙여넣고 끝에 /oauth2/token을 추가합니다
#### &nbsp;&nbsp;&nbsp;&nbsp; https://yckim-app.auth.ap-northeast-2.amazoncognito.com/oauth2/token 이렇게 꼭 추가하세요!!!!!

#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 Client ID, Client Secret은 Cognito 앱 클라이언트 > 세부 정보 표시에서 확인할 수 있어요 복붙합시다

#### &nbsp;&nbsp;&nbsp;&nbsp; 마지막 Scope는 위의 OAuth 범위 항목에서 설정한 범위 이름이 쓰입니다
#### &nbsp;&nbsp;&nbsp;&nbsp; 자 그리고 토큰을 요청해봅시다!!!!
![lambda-1](/img/post/20181213/lambda-15.png )

#### &nbsp;&nbsp;&nbsp;&nbsp; 토큰이 발급되었습니다 스크롤 내려서 Use Token을 누르면 Headers탭에 Authorization 항목으로 자동으로 추가됩니다

![lambda-1](/img/post/20181213/lambda-16.png )
#### &nbsp;&nbsp;&nbsp;&nbsp; 그리고 다시 API 요청을 하면 Hello from Lambda가 출력되는걸 확인 할 수 있습니다
