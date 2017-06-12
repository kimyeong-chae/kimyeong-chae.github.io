---
layout: post
title:  "Jekyll을 이용한 블로그 만들기! (1)"
date:   2017-06-12 21:47:21 +0900
categories: tech
---

## 블로그 만들기전 알아야 할 것 및 해야할 일
------
#### Markdown
간단하게 HTML보다 쉬운 문법으로 웹페이지를 만들 수 있는 언어라고 생각한다
예를들어 HTML에서 테이블을 만들 경우와 마크다운 언어로 만들 경우를 비교해보면

```html
<h1>html로 table만들기</h1>
<table>
  <thead>
    <tr>
      <td></td>
    </tr>
  <thead>
  <tbody>
    <tr>
      <td></td>
    </tr>
  </tbody>
</table>
```

```Markdown
Markdown 문법으로 table만들기

헤더|헤더|헤더
-|-|-
내용|내용|내용
```

누가봐도 아래가 간단하다. 이런 언어다.

#### Jekyll
그렇다면 `Jekyll`이 뭐냐라고 한다면 `Markdown`언어를 웹페이지로 만들어주는 파싱엔진 이라고 한다.
자세한건 <https://jekyllrb-ko.github.io/> 에서 확인하시면 된다.

#### GitHub
분산 버전관리 툴인 git을 사용하는 프로젝트를 지원하는 웹 호스팅 서비스이다.
자세한건 <https://ko.wikipedia.org/wiki/%EA%B9%83%ED%97%88%EB%B8%8C>에서 확인 하시면 된다.
일단 가입을 해야한다.
  * <https://github.com/> 접속

![github 홈페이지](/img/post/20170612/github.png )
  * sign up for GitHub 클릭 후 진행

![github 가입](/img/post/20170612/signup.jpg )

여기까지 하면 일단 끝!
