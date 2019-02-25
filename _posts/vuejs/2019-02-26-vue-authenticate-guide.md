---
layout: post
title:  "vue-authenticate 가이드"
date:   2019-02-26 02:00:21 +0900
categories: vuejs
author : yckim
---

# vue-authenticate 모듈 소셜 로그인 가이드    
  
## 배경  
  
### vue.js로 Single Page Application 토이 프로젝트 작업 중 사용자 인증 작업이 필요한 상황이였고,  

### local-login은 필요 없고 소셜 로그인 기능만 필요했다  


### 적당한 모듈을 찾아보던 중 vue-authenticate가 다운로드 수가 가장 많고,   

### 다양한 소셜 로그인을 지원하고 있어서 이 모듈로 결정하게 됨  

_ _ _

### Frontend(Vue.js) 설정    
  
  
### 소셜 로그인은 Google, Facebook, Instagram을 사용했고, 미리 각 사이트에서 앱을 생성했다고 가정    



### 1. vue-authenticate 모듈 설치  
`$ npm i --save vue-authenticate`  
  

### 2. vue-router 설정  
![1](/img/post/20190226/2.png )  
  
### vue-router 가장 하단에 추가함


### 3. vue.js instance 설정파일에서 vue-authenticate 설정 추가  
![1](/img/post/20190226/1.png )
### **redirectUri는 위의 2번에서 설정한 path로 해주면 된다**  


### 4. login component에서 methods 추가  
![1](/img/post/20190226/3.png )  
### 나의 경우 각 사이트에서 로그인 성공 후 프로필 정보를 받은 후 TODO문에서 backend passport로 로그인 시켰음  


### 5. 적절한 태그에 위의 method 호출하게 수정  

```
<div @click="authenticate('google')">
<div @click="authenticate('facebook')">
<div @click="authenticate('instagram')">
```
  

### 이것으로 Vue.js(Frontend) 설정은 끝났다  

_ _ _

## Backend(Node + Express) 설정
 

### 1. login router 설정
```
/**
 * social login callback
 */
router.post('/auth/:provider', function(req, res){
    switch(req.params.provider) {
        case 'facebook':
            facebookAuth(req, res)
            break
        case 'google':
            googleAuth(req, res)
            break
        case 'instagram':
            instagramAuth(req, res)
            break
        default:
            res.sendStatus(400);
            break;
    }
});

/**
 * facebook get access_token
 */
function facebookAuth(req, res) {
    axios.post('https://graph.facebook.com/v2.4/oauth/access_token', {
        client_id: config.auth.facebook.clientId,
        client_secret: config.auth.facebook.clientSecret,
        grant_type: 'authorization_code',
        code: req.body.code,
        redirect_uri: req.body.redirectUri
    }, { 'Content-Type': 'application/json' }).then((response) => {
        var responseJson = response.data
        res.json(responseJson)
    }).catch((err) => {
        res.status(500);
    })
};

/**
 * google get access_token
 */
function googleAuth(req, res) {
    Request({
        method: 'post',
        url: 'https://accounts.google.com/o/oauth2/token',
        form: {
            code: req.body.code,
            client_id: config.auth.google.clientId,
            client_secret: config.auth.google.clientSecret,
            redirect_uri: req.body.redirectUri,
            grant_type: 'authorization_code'
        },
        headers: {
            'content-type': 'application/x-www-form-urlencoded'
        }
    }, function (err, response, body) {
        try {
            if (!err && response.statusCode === 200) {
                var responseJson = JSON.parse(body);
                res.json(responseJson)
            } else {
                res.status(response.statusCode).json(err)
            }
        } catch (e) {
            res.status(500).json(err || e)
        }
    })
};

/**
 * instagram get access_token
 */
function instagramAuth(req, res) {
    Request({
        method: 'post',
        url: 'https://api.instagram.com/oauth/access_token',
        form: {
            code: req.body.code,
            client_id: config.auth.instagram.clientId,
            client_secret: config.auth.instagram.clientSecret,
            redirect_uri: req.body.redirectUri,
            grant_type: 'authorization_code'
        },
        headers: {
            'content-type': 'application/x-www-form-urlencoded'
        }
    }, function (err, response, body) {
        try {
            if (!err && response.statusCode === 200) {
                var responseJson = JSON.parse(body)
                res.json(responseJson)
            } else {
                res.status(response.statusCode).json(err)
            }
        } catch (e) {
            res.status(500).json(err || e)
        }
    })
}
```

### 이렇게 설정해주면 끝!

----

