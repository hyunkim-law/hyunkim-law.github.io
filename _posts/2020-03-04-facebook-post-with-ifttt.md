---
layout: post
title: "IFTTT를 이용하여 커맨드라인에서 페이스북에 포스팅하기"
categories: ["how"] # suggestion: gtd, how, lawyering, news, stuff, books
excerpt: "IFTTT를 이용하여 커맨드라인에서 한글로 페이스북에 포스팅하기"
sharing:
  facebook: "IFTTT를 이용하여 커맨드라인에서 한글로 페이스북에 포스팅하기 삽질"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-04 03:56:08 +0900
tags: 
math: # true possibly
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
bibliography:
---

옛날부터 리눅스에서 명령어줄을 열어 놓고, 그 명령어줄에서 작업하는 것을 좋아했었죠.  생각해보니, 제가 페이스북을 안하는 가장 큰 이유는 사실 그게 안되기 때문이죠. 원래는 됐었는데, 이제는 페이스북에서 그걸 막았다고 하더라구요. `FBCMD`라고 했었는데, 이제는 막혔죠. 방법이 있긴 있습니다. [IFTTT](https://ifttt.com)을 이용하는 것인데, 앞의 [페이스북 포스팅 자동화](/blog/2020/03/facebook-sharing.html)에서 한 것은 `IFTTT`의 기존의 레시피를 이용하는 것이었죠. 따라서, 제 블로그에서 작업은 좀 까다롭지만, 정작 `IFTTT`에서는 마우스 몇 번만 클릭하면 됐었죠. 이제는 그게 아니라, 명령어줄에서 직접 페이스북에 포스팅을 하는 겁니다. 이걸 하기 위해서는 [webhook](https://ifttt.com/maker_webhooks)이라는 것을 이용해야 합니다. `webhook`을 이용하려면, 위 페이지에서 맨 위의 `Documentation`을 클릭해 가 보면, 본인의 키 그러니까 비밀번호와 간단한 사용법이 있습니다. 이걸 가지고 간단히 만들어 보죠.  일단 키를 별도의 파일에 저장합니다. 파일 이름을 `key`라고 하죠. 그 다음에, 위의 페이지의 예에 있는 대로 해 보죠.

{% highlight bash linenos %}
curl -X POST https://maker.ifttt.com/trigger/{event}/with/key/{key}
{% endhighlight %}

그 다음에는 `IFTTT` 홈페이지에서 `Explore`로 가서 `Make your own Applets from scratch`를 클릭합니다. 여기서 `IF`를 선택하면 `Choose a service`라는 곳으로 가는데, 검색에 `webhooks`를 클릭하고, `Receive a web request`를 클릭합니다. 그러면 `Event Name`을 입력하라고 나오는데 아무 이름이나 입력하고 `Create trigger`를 선택합니다. 예를 들어, `test`이라는 이름을 선택했다고 해 보죠. 그러면 위 주소는 이렇게 됩니다.

{% highlight html linenos %}
https://maker.ifttt.com/trigger/test/with/key/{key}
{% endhighlight %}

그리고 위의 `{key}` 자리에 위에서 저장한 키를 넣으면 되는거죠. 명령어로 한 번 해 보죠. 주의할 점은 아래 명령에서는 한글은 먹히지 않는다는 점입니다.

여기서 한 가지 더 해야 되는데, `THEN`을 선택한 다음에, `facebook status message`를 선택하고 `Status message`항에 `Value1`을 선택합니다.

{% highlight bash linenos %}
$ curl -X POST https://maker.ifttt.com/trigger/test/with/key/{key}?value1="How?"
{% endhighlight %}

일단 이렇게 하면 되긴 합니다. 그 다음에는 극복해야 하는 문제가 두 가지가 있는데 첫째는 공백을 입력할 때에는 반드시 `%20`를 입력해야 한다는 것이고, 두번째는 한글은 거의 깨진다는거죠. 그리고, `json`으로 보낼 때는 따옴표 정리하는게 정말 머리아프다는 겁니다 (게다가 나중에 `bash` 스크립트 만들 때는 변수와 관련된 따옴표 문제도 또 생기죠. 몇 번 시행착오를 거쳐서 결국 찾아낸 솔루션은 이겁니다. `json`을 큰따옴표로 다 감싸고, 그 속에도 큰 따옴표를 써야 하지만, 이건 모조리 이스케이프하는거죠. 말은 쉽지만, 작은 따옴표와 큰 따옴표의 온갖 조합을 다 해본 것 같습니다.

{% highlight bash linenos %}
$ curl -H "Content-Type: application/json" -X POST -d "{\"value1\": \"여기에 포스팅할 내용을 입력한다\"}" https://maker.ifttt.com/trigger/test/with/key/{key}
{% endhighlight %}

그러니, 이제 간단한 `bash` 스크립트를 만들어 보면, 이렇게 되겠죠. 위에서 키를 `key`라는 파일에 저장해 두었다고 하면,

{% highlight bash linenos %}
#!/bin/bash
string=$1
key=`cat ~/key`
address="https://maker.ifttt.com/trigger/fbtext/with/key/"

curl -H "Content-Type: application/json" -X POST -d "{\"value1\": \"${string}\"}" $address$key
{% endhighlight %}

두 번째 줄에서는 입력하는 것을 받아서 `string`이라는 변수에 저장, 세 번째 줄에서는 `key` 파일을 읽어서 `key`라는 변수에 저장, 그 다음줄은 주소 앞부분을 `address`라는 변수에 저장하고, 맨 마지막 줄에서는 이걸 가지고 보내는 메시지를 조합하는거죠. 쉽죠. 나름 시행착오를 거치긴 했지만, 나름 뭐 유용하게 쓰겠네요. 포스팅은 이렇게 합니다.

{% highlight bash linenos %}
$ postfb "여기에 포스팅할 내용 포함"
{% endhighlight %}