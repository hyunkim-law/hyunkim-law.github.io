---
layout: post
title: "페이스북 포스팅 자동화"
categories: [how]
date: 2020-03-01 15:30:00 +0900
excerpt: "RSS와 IFTTT를 이용하여 블로그에 글이 올라올 때마다 자동으로 페이스북에 포스팅하기"
#sharing: 
#  facebook: "지킬에서 페이스북 포스팅 자동화하기"
color-scheme: brown
postimage: fb.png
---

페이스북을 그렇게 좋아하지 않는다. 그러니까, 페이스북은 적극적으로 사용하지 않고 소극적으로만 사용하고 있다. 이걸 좀 바꿔 보려고 한다. 지금까지 소극적으로만 사용한 이유는 주로, 아마도 귀차니즘, 새로운 것을 배우기 싫어하는 마음이었던 것 같다.

첫 시도는 페이스북 포스팅을 자동화하는 것으로 해 보려 한다. [이 페이지](https://www.jflh.ca/2017-02-08-how-i-automate-social-media-sharing-of-my-jekyll-blog-articles)에 있는 것을 그대로 따라해 보았다. 아이디어는 홈페이지에 굳이 `RSS` 피드가 하나만 있어야 하는 것은 아니라는 것이다. 전체적인 흐름은 우선 페이스북 포스팅 전용 `RSS` 피드를 만드는 것이다. 그 다음에는 이것을 이용해서 포스팅을 쓰는 방법이고, 마지막은 [IFTTT](https://ifttt.com/)라는 것을 이용하여 포스팅을 할 때마다 페이스북에 글을 쓰도록 하는 것이다. `IFTTT`는 **If This Then That**의 줄임말인데, "이런 일이 생기면 저런 일을 하라"는 뜻이다. 사실 페이스북 포스팅 용도 이외에도 꽤 유용하다. 당연히 이것은 [지킬](https://jekyllrb.com/) 블로그를 이용한 것이다.

### 피드 RSS 만들기

위 포스트에 따르면, `RSS` 피드를 따로 만들라고 하는데, 이 과정은 만약 자기가 포스팅하는 모든 내용을 페이스북에 올리려는 사람은 넘어가도 좋다. 또, 저자는 트위터, 페이스북 및 링크드인 세 개의 피드에 대하여 각각 만들라고 하는데, 그가 한 것을 보면 이해는 되지만, 굳이 이렇게까지 할 필요가 있을지는 잘 모르겠다. 

우선 `_layout` 디렉토리에 `sharing_feed.xml`이라는 파일을 만든다. 지킬에서 `_layout` 디렉토리에 들어있는 것은 여러 컨텐츠에서 공유할 수 있는 일종의 템플릿 역할을 한다.

{% highlight xml linenos %}{% raw %}---
---
<?xml version="1.0" encoding="UTF-8"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <title>{{ site.title | xml_escape }}</title>
    <description>{{ site.description | xml_escape }}</description>
    <link>{{ site.url }}/</link>
    <atom:link href="{{ page.url | absolute_url }}" rel="self" type="application/rss+xml" />
    <pubDate>{{ site.time | date_to_rfc822 }}</pubDate>
    <lastBuildDate>{{ site.time | date_to_rfc822 }}</lastBuildDate>
    <generator>Jekyll v{{ jekyll.version }}</generator>
    {% assign posts = site.posts | where_exp: "post", "post.sharing[page.sharing_site]" %}
    {% for post in posts limit:5 %}
      <item>
        <title>{{ post.sharing[page.sharing_site] | xml_escape }}</title>
        <pubDate>{{ post.date | date: "%a, %d %b %Y %H:%M:%S %z" }}</pubDate>
        <link>{{ post.url | absolute_url }}</link>
        <guid isPermaLink="true">{{ post.url | absolute_url }}</guid>
      </item>
    {% endfor %}
  </channel>
</rss>{% endraw %}{% endhighlight %}

여기에서 가장 중요한 부분은 13번째 줄이다. 여기에서 `post.sharing[page.sharing_site]`라고 되어 있는 부분은 포스트를 쓸 때 공유할 사이트와 각 사이트별로 지정할 제목(즉 전달할 메시지)를 다르게 할 수 있다는 점이다. 따라서, 실제 포스트의 `frontmatter`에는 다음과 같이 들어가게 된다.

{% highlight yaml linenos %}
---
title: 제목이 들어가는 곳
sharing:
  twitter: 트위터에 보낼 메시지
  facebook: 페이스북에 보낼 메시지
  linkedin: 링크드인에 보낼 메시지
---
{% endhighlight %}

마지막으로, 위에서는 레이아웃만 만든 것이므로 실제 전달할 `xml`을 만든다. 예를 들어, 페이스북의 경우라면, 다음과 같이 두 줄이 들어간 파일을 만들고, 이름을 `facebook.xml` 또는 원하는 이름을 붙이면 된다.

{% highlight yaml linenos %}
---
layout: sharing_feed
sharing_site: facebook
---
{% endhighlight %}

### IFTTT

앞에서 말한 것처럼, 이 곳은 어떤 것을 감시하다가 (IF) 미리 지정한 사건(THIS)이 생기면(THEN) 이런 일을(THAT) 하도록 하는 아주 유용한 프로그램이다.  사용법은 아주 직관적이다.

여기에서 페이스북의 경우에는 **THIS**는 서비스 RSS를 고르고 주소를 입력한다. 만약 `facebook.xml`이라고 파일명을 정했다면, 자기 주소 뒤에 이것을 덧붙인다 (예: https://hyunkim.lawyer/facebook.xml). **THAT** 부분에는 서비스는 Facebook을 고르고 할 일(action)은 "링크 포스트 만들기(create a link post)"를 선택, 주소와 제목 등 포함될 내용을 선택하면 된다. 예를 들어, `Message` 부분에는 {% raw %}{{EntryTitle}}{% endraw %}과 같이 입력하는 것이다.