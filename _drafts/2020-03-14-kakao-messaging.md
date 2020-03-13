---
layout: post
title: "카카오 API를 이용하여 메시지 보내기"
categories: [" how"] # suggestion: gtd, how, lawyering, news, stuff, books, english
excerpt: "카카오 API를 이용하여 메시지 보내기"
sharing:
  facebook: "카카오 API를 이용하여 메시지 보내기"
  twitter: "카카오 API를 이용하여 메시지 보내기"
  linkedin: "카카오 API를 이용하여 메시지 보내기"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-14 03:46:10 +0900
tags: 
math: # true possibly
header-img: lawbook.jpg
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
---

인터넷을 찾아보면 많이 나오는데, 헷갈리기도 하고, 오래되서 내용이 약간 안맞는 것도 많아서, 정리해 두는 게 좋겠다는 생각이 들어서... 가장 중요한 것은 토큰을 받는 것이다.

그러기 위해서는 개발가이드의 [카카오 로그인](https://developers.kakao.com/docs/js/kakaologin)을 참고하여, 로그인이 가능한 페이지를 하나 만들어야 한다. 그리고, 로그인 페이지를 가기 전에(!)

우선 개발자 가입 후 [애플리케이션](https://developers.kakao.com/apps) 페이지에 가서 애플리케이션을 만들고 (애플리케이션이 특별한 것은 아닌게, 그냥 홈페이지도 자바스크립트 애플리케이션이다), 앱 키를 받아 둔다. 그리고, 카카오로그인을 활성화하고 `로그인 Redirect URI`를 앞에서 만든 로그인이 가능한 페이지로 지정해 준다.

그 다음에는, [사용자 관리](https://developers.kakao.com/docs/restapi/user-management) 페이지를 참고하여, 사용자 토큰을 받는다. 이것을 위해서는 우선 `권한키`를 발급받아야 한다. 그러니까, 무지 헷갈리는데, `권한키(authorize key)`를 받고 나서는 이걸 이용해서 `접속키(access key)`를 발급받을 수 있다. 우선 첫단계, 그러니까 `권한키`를 받기 위해서는 앞에서 받아 둔 앱키가 필요하다. 이걸 이용해서,

~~~bash
$ curl -X POST https://kauth.kakao.com//oauth/authorize?client_id={app key}&redirect_uri={redirect uri}&response_type=code
~~~

와 같이 해 준다. 위에서 `{app key}`라고 적힌 곳에 앱 키를, 그리고 `{redirect_uri}`라고 적힌 부분에 `로그인 Redirect URI`를 넣는다. 그렇게 명령을 주고 나서, `Redirect URI`에 기입한 카카오 로그인 버튼이 있는 곳을 가서, 모든 것에 동의해 주고 나면, `json` 파일이 나온다. 그 형식은 대략 다음과 같다.

~~~json
{"access_token":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx","token_type":"bearer","refresh_token":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx","expires_in":1111,"scope":"account_email story_read talk_message profile story_publish","refresh_token_expires_in":1111111}
~~~

여기에서 `"access_token"` 에 있는 부분이 우리가 원하는 액세스 토큰이다. 

이 페이지에 있는 내용을 그대로 복사하자면,

~~~bash
curl -v -X POST https://kauth.kakao.com/oauth/token \
 -d 'grant_type=authorization_code' \
 -d 'client_id={app_key}' \
 -d 'redirect_uri={redirect_uri}' \
 -d 'code={authorize_code}'
 ~~~

 위에서 중괄호에 든 `{app_key}` 부분에는 자기 앱 키를, `{redirect_uri}` 부분에는 위에서 받은 `로그인 Redirect URI`를 넣어 준다. 명령어 줄에서 실행하고 나서, 


 참고 페이지:

- [카카오 로그인](https://developers.kakao.com/docs/js/kakaologin)
- [사용자 관리](https://developers.kakao.com/docs/restapi/user-management)
- [카카오톡](https://developers.kakao.com/docs/restapi/kakaotalk-api#%EB%82%98%EC%97%90%EA%B2%8C-%EB%B3%B4%EB%82%B4%EA%B8%B0)