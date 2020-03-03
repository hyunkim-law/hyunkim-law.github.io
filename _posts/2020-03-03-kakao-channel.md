---
layout: post
title: "홈페이지에 카카오채널 붙이기"
categories: ["how"] # suggestion: gtd, how, lawyering, news, stuff, books
excerpt: "홈페이지에 카카오채널 붙여서 카카오로 대화하기"
sharing:
  facebook: "카카오채널을 이용하여 홈페이지 방문객과 대화하기"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-03 23:28:23 +0900
tags: 
math: # true possibly
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
---

좀 헷갈리긴 합니다. 일단 [카카오 개발자홈페이지](http://developers.kakao.com)로 가서 회원가입을 합니다. 이 까지는 그렇게 어렵지 않죠. 그 다음에는 [새로운 앱을 만들기](https://developers.kakao.com/apps/new) 시작합니다. 앱에는 세 가지가 있는데, iOS나 Android 앱을 만들게 아니라면, 그냥 JavaScript 앱을 만듭니다. 딱히 앱이라기보다는 홈페이지에 제 홈페이지에 보이는 것 같은 카카오채널을 이용하기 위해 자바스크립트를 활용하는 겁니다. 헷갈리면 [개발가이드](https://developers.kakao.com/docs/js/getting-started)를 참고합니다.

자바스크립트 앱을 만들고 나면, `설정-일반`으로 가서 플랫폼에 웹을 추가하고, 도메인을 입력합니다. 그 다음에는 시키는 대로 링크를 따라 사용자관리로 가서 `로그인 Redirect URI`에 사용할 페이지 주소를 모조리 입력합니다. 예를 들어, [https://hyunkim.lawyer](https://hyunkim.lawyer) 뿐 아니라, [https://hyunkim.lawyer/contact.html](https://hyunkim.lawyer/contact.html) 등등과 같이 세부적인 웹사이트 주소를 모두 입력하라는거죠. 10개까지... 그걸 넘어가면 별도로 연락을 하고... 그 다음에는 개요의 앱키/설정-일반의 앱키(같은 겁니다)에서 앱키를 받아 둡니다. 

그 다음에는 [설명서의 카카오채널](https://developers.kakao.com/docs/js/kakao-talk-channel)에 있는 것처럼, 위의 앱키와 더불어 다른 정보가 하나 더 필요한데, 이건 [카카오톡 채널 관리자센터](https://center-pf.kakao.com/)로 가서 새로운 채널을 하나 만들어야 합니다. 만든 채널로 가서, 아래쪽의 `관리-상세설정`으로 가면, `홈 URL`이 있습니다. 여기 주소는 다음과 같이 되어 있죠.

{% highlight html linenos %}
http://pf.kakao.com/_abcdefg
{% endhighlight %}

여기에서 뒤쪽의 주소를 어디 적어 둡니다. 그리고는 위 카카오채널 매뉴얼의 코드를 복사/붙여넣기 하여 여기에 홈 URL과 앱키를 입력합니다. 설명서에서 그대로 복사해 오면,

{% highlight javascript linenos %}
<script type='text/javascript'>
  //<![CDATA[
    // 사용할 앱의 JavaScript 키를 설정해 주세요.
    Kakao.init('YOUR APP KEY');
    function chatChannel() {
      Kakao.Channel.chat({
        channelPublicId: '_xcLqmC' // 카카오톡 채널 홈 URL에 명시된 id로 설정합니다.
      });
    }
  //]]>
</script>
{% endhighlight %}

이 부분인데, 네번째 줄의 `kakao.init`의 `YOUR APP KEY` 부분에 앱 키를 넣고, 일곱번째줄의 `channelPublicID`에 `홈 URL`을 넣는거죠. 이걸 홈페이지에 붙여 넣으면 됩니다. 쉽네요. 그렇지만, 막상 그리 만만치는 않습니다. 헷갈려서...

아니면, 개발가이드에서 아래쪽으로 내려가서 `소셜 플러그인` 아래 [카카오톡 채널 추가하기](https://developers.kakao.com/docs/social-plugins/kakao-talk-channel-add) 페이지에서 시키는 대로 입력하고 `코드 생성하기`를 눌러도 됩니다. 이게 더 쉬울 수도 있겠네요. 그리고, 생성되는 코드를 자기 홉페이지에 넣어 줍니다. 코드가 두 개가 나오는데 시키는 대로 붙여 넣어주면 됩니다.