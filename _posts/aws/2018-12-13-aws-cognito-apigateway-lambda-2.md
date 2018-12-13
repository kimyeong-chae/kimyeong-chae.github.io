---
layout: post
title:  "AWS Lambda + Api Gateway + Cognito 설정해보기(2)"
date:   2018-12-13 22:41:21 +0900
categories: aws
author : yckim
---


이전글에서 Cognito 설정을 했고 이번글에서는 **Lambda + Api Gateway** 설정 후 **Cognito**롤 엮는 설정까지 해보겠습니다



### Lambda 함수 추가

##### &nbsp;&nbsp;&nbsp;&nbsp; Lambda > 함수 > 함수 생성
###### &nbsp;&nbsp;&nbsp;&nbsp; 이름 입력하고, 역할은 *1개이상의 템플릿에서 새로운 역할을 생성합니다* 선택하고 *함수 생성*
![lambda-1](/img/post/20181213/lambda-1.png )
