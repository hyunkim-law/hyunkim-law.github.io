---
layout: page
title: 지킬(Jekyll)로 홈페이지/블로그 만들기
author: Hyun Kim
category: web
order: 002
---

## 목차
{:.no_toc}

* ToC
{:toc}

---

## 성질 급한 사람을 위한 요약

~~~bash
$ gem install jekyll bundler
$ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle install
~/my-awesome-site $ bundle exec jekyll serve
# => 인터넷 브라우저에서 http://localhost:4000 로 가기
~~~

설명하자면, 첫번째 명령어는 **jekyll**과 **bundler**를 설치한다 (여기에서는 루비의 패키지 관리 도구인 [ruby bundler](http://bundler.io/)를 사용한 것을 전제로 한다.[^fn1])[^fn2]  

[^fn1]: 루비에서 가장 골치 아픈 문제가 패키지 관리이다.  패키지 관리 도구에는 [rvm](https://rvm.io/)과 [rbenv](http://rbenv.org/)가 있었는데, 요즘은 **bundler**로 옮아가는 추세이다.  오픈소스를 배우면서 염두에 두어야 하는 것은 언제나 대세를 따라야 한다는 것이다.

[^fn2]: 여기 예는 [지킬 홈페이지](https://jekyllrb.com/)의 예를 그대로 이용한 것이다.  아래에서도 대개의 내용은 [지킬 문서](https://jekyllrb.com/docs/home/) 내용을 기초로 하여 작성한 것이다.

두번째 명령어는 지킬을 이용하여 새로운 사이트를 만드는 것이다.  *my-awesome-site* 부분은 각자 원하는 이름으로 바꿔 주면 된다.  그대로 써도 무방하다.  사이트 자체의 이름이나 주소와는 무방하므로, 아무 이름이나 써도 좋다.  이 명령을 실행하면, 지킬은 이름으로 정한 디렉토리를 만들고, 기본적으로 필요한 파일을 생성해 준다.  세번째 명령어는 그 디렉토리로 진입하는 것이다.

네번째와 다섯번째의 시작부분이 **$** 표시가 아닌 디렉토리 이름으로 적은 것은 그 디렉토리에 있다는 것이다.  네번째 명령어는 **bundler** 패키지를 이용하여 여기에 필요한 다른 젬[^fn3]을 설치하도록 하는 것이다.  그리고, 그 다음 명령어는 지킬을 시작하는 것이다.  마지막 줄은 셸이 아니라 웹 브라우저를 열고, 웹 브라우저에서 해당 주소로 가 보라는 뜻이다.  더 자세한 사항은 [지킬 문서](https://jekyllrb.com/docs/home/) 페이지를 참고하라 (이 글도 대체로 이 문서 페이지의 내용을 참고하여 정리하였다).  성질도 급하고, 시간도 없다면, 여기에서 중단해도 좋다.  아래에서는 그렇지 않은 사람, 즉 성질도 착하고 시간도 남아 도는 사람을 위해 (다소) 길게 좀 더 자세히 정리하였다.

[^fn3]: [루비 프로그래밍 언어](https://www.ruby-lang.org/en/)에서는 gem을 이용하여 패키지를 관리한다 (RubyGem이라고 한다).  루비는 보석(gem)이라서, 아마도?

## (시간이 남아 도는 사람을 위한 상세한 설명) 파괴력 있는 수박겉핧기

[페이스북](http://www.facebook.com)도 있고, [트위터](http://www.tweitter.com)도 있고, [미디엄](http://www.medium.com)도 있고, [브런치](http://www.brunch.co.kr)도 있는데 왜?  동의한다.  글을 쓰고, 글과 멀티미디어로 관계맺기를 하는 것이 목표라면, 모두 아주 좋은 전략이다.  게다가 간편하고, 따로 배워야 하는 것도 없고, 따로 돈을 낼 필요도 없다.  사소한 문제라면, 글의 휘발성이 너무 높다는 것 (20초의 영광을 위하여 며칠동안 공들여 비디오 만드는 것을 생각해 보라), 컨텐츠나 포맷을 사용자가 직접 통제할 수 없으며, 그래도 어쨌건 홈페이지는 필요한 게 현실이다 (페이스북 페이지가 있다고 해서 홈페이지를 폐쇄하는 회사를 본 적이 있는가?).

나는 성격 때문에, 또 취향 때문에 많은 종류의 블로그 소프트웨어를 사용해 봤다.  그리고 나는 지킬에 안착하였다.  홈페이지나 블로그를 만들고 싶은 사람이라면 현재로서는 나와 마찬가지로 지킬을 써야 한다고 생각한다.  약점이라면, 좀 배워야 하는 것이 많다.  예를 들어, 

- html, css, 자바스크립트
- 루비, 루비젬스 (rubygems: 보석쪼가리)
- 터미널에서 명령어 입력하기
- 텍스트 편집기 사용하기
- 마크다운, 리퀴드
- 호스팅 및 클라우드 관련 명령어

걱정할 필요는 없다.  배워야 하는 것은 아주 많지만, 여러분의 목표가 단지 홈페이지 내지는 블로그 하나 만드는 거라면 여러분의 목표는 이 모든 것을 다 알아 내는 것이 아니라, 수박겉핧기로 대충, 빠르게, 기초만 배우는 것이다.  지킬이라는 소프트웨어는 그러라고 만든 것이다.  이 글도 그래서 쓴 것이다.  다소 길지만, 꼭 알아야 하는 것만 수박겉핧기로 알고 넘어갈 수 있도록 정리하였다.

## (시간이 남아 도는 사람을 위한 상세한 설명) 그래서, 지킬이 뭔데?

[지킬 홈페이지](https://jekyllrb.com/docs/home/)에 따르면, 지킬은 "간단한 블로그가 되는 정적 사이트 생성기 (simple, blog-aware, static site generator)"이다.  무슨 말인지 모르겠다면, 그게 정상이다.  소프트웨어는 아무리 문서를 읽어 봐야 무슨 뜻인지 모를 수 밖에 없다.  일단 해 봐야 한다.  그 다음에 문서를 읽는 것이 순서이다.

그래도 궁금한 사람을 위해 조금만 부연설명하자면, 사이트란 홈페이지이다.  사이트 생성기란 홈페이지를 만든다는 것이다.  어떻게 만들까?  아는 사람은 알겠지만, 홈페이지는 *html* 이라는 언어로 만들어진다.  이건 *HyperText Markup Language,* 즉 하이퍼텍스트 ("링크가 있는"이라고 이해하면 간단하다)로 작성한 마크업을 하는 (프로그래밍) 언어라는 뜻이다.  요즘은 여기에 더하여 자바스크립트와 CSS 등이 사용되기도 한다.  옛날보다 복잡해졌지만, 옛날보다 훨씬 더 복잡한 것도 구현할 수 있게 된 것이다.  

마크업 언어는 무엇인가?  마이크로소프트 워드를 써 본 적이 있을 것이다.  마이크로소프트 워드에서 글의 포맷을 바꿀 때 (예를 들어 밑줄을 칠 때) 바꿀 부분을 마우스로 선택한 다음, 밑줄을 치는 단축키 (Ctrl + u) 누르거나, 아니면 메뉴의 밑줄 아이콘을 클릭한다.  그러면, 선택한 부분이 바뀐다.  이런 방식을 WYSWYG (What you see is what you get)이라고 한다.  하는 대로 바뀌고, "보이는 대로 결과가 나온다는" 것이다.  이런 용어가 있다는 것은 그렇지 않은 것도 있다는 뜻이다.  이전에는 더 불편했는데, 이제는 더 좋은 방법을 찾았다는 의미에서 사람들이 그렇게 이름을 붙인 것이다 (나는 당연히 동의하지 않는다).  그 이전에는 사람들이 어떻게 했을까?  마크업 언어를 사용했다.  예를 들어, 텍스트 파일에 이렇게 입력하는 것이다.

~~~html
<u>밑줄을 칠</u> 부분
~~~

그 즉시 밑줄이 쳐지지 않는다. 당연하다.  html은 WYSWYG가 아닌 것이다.  그 대신 텍스트 파일을 만들어서 *html* 확장자를 붙여서 저장한 다음, 이 파일을 웹브라우저에서 열면 내용이 보일 것이고, 여기에서 *u* 로 앞뒤로 막은 부분은 밑줄이 쳐져 있을 것이다.  이것이 마크업이다.  그리고, 마크다운은 마크업의 반대이다.

반대라기보다는, 마크다운은 마크업이 너무 복잡하다고 느껴지는 사람을 위해서 문법을 좀 더 간단히 바꾼 것이다.  밑줄의 예는 너무 간단하므로 링크를 붙이는 예를 들자면, html에서는

~~~html
<a href="http://hyunkim.lawyer">홈페이지</a>
~~~

처럼 하겠지만 (마크업), 마크다운에서는 

~~~markdown
[홈페이지](http://hyunkim.lawyer)
~~~

과 같이 한다.  좀 더 간단해졌다.

홈페이지를 만들자면, html을 알아야 하고, css를 알아야 하고, 자바스크립트를 알아야 한다.  게다가, 똑같은 모습을 가진 페이지를 만들려면 (스킨) 똑같은 코드를 반복해서 입력해야 한다.  지킬을 사용한다고 해서 이걸 몰라도 된다는 뜻은 아니다.  지킬이 홈페이지 생성기라는 뜻은 그 대신 [마크다운](https://daringfireball.net/projects/markdown/)과 [liquid](https://github.com/Shopify/liquid/wiki)처럼 훨씬 간단한 문법을 사용하는 언어를 이용해서 페이지를 구성하고 나면, 알아서 html, css, 자바스크립트로 구성된 홈페이지로 바꾸어 준다는 뜻이다.

블로그란 대체로 개인 홈페이지로 이해되지만, 특정한 규칙에 따라 (예를 들어, 가장 최근 글이 가장 위로 올라오는) 내용을 정리해 주는 홈페이지 생성기이다.

정적이라는 것은 무엇인가?  위에서 마크업/마크다운 이야기를 할 때처럼, 기술적인 용어는 무엇이 그게 **아닌지** 이해하면 그게 무엇인지 더 잘 알 수 있는 경우가 많다.  기술 발전의 본질이 과거의 불편함을 "개선"하고 바꾸는 것이기 때문이다.  대부분의 블로그 소프트웨어는 **동적** 홈페이지 생성기이다.  대표적인 예가 가장 많이 사용하는 [워드프레스](http://wordpress.org)이다.  동적 홈페이지 생성기는 미리 홈페이지 (html 등의 파일)을 만들어 두지 않는다.  사용자가 홈페이지에 접속을 하면, 즉 페이지를 요청하면, 그때야 홈페이지를 만들어서 사용자에게 보내 준다.  이게 왜 좋을까?  홈페이지 내용이 끊임 없이 변하는 것을 생각해 보자.  예를 들어, 이메일이나 채팅 서비스 페이지 같은 곳.  내지는 검색이나 소셜 네트워크 같은 곳.  내지는 온라인 편집기와 같은 애플리케이션들.  내용이 항상 변화한다면, 굳이 매번 정적인 페이지를 만들어 두는 것은 의미가 없다.  그러므로, 이런 페이지는 동적 페이지를 만들어야만 한다.

블로그는 어떤가?  내용이 제법 자주 변화한다.  예를 들어, 네이버와 같은 포털에서 제공하는 블로그를 생각해 보자.  매순간 변화한다.  개인 페이지는 어떤가?  많이 변해야 하루에 한 번 내지는 두세번일 것이다.  정말 많이 변해도 한 시간에 한 번 이상 변화하는 것은 생각하기 어렵다.  그런데, 동적 웹페이지를 사용해야 하는가?  그렇다.  아니, 그랬었다.  여기에는 두 가지 이유가 있다.  첫째, 모든 블로그 소프트웨어에는 온라인 편집기가 포함되어 있다.  온라인으로 글을 쓰는 곳을 찾아가서 거기에서 글을 쓴다면, 그 페이지는 동적일 수 밖에 없다.  그리고, 두번째는 다소 역사적인 이유이다.  과거에는 홈페이지를 만들 때 대부분 [아파치](https://en.wikipedia.org/wiki/Apache_HTTP_Server)라는 웹 서버 프로그램을 사용했었다.  그리고, 과거에 대부분의 개인 홈페이지를 운영하는 취미꾼들과 블로거들은 거의 공유 호스팅이라는 것을 사용했었다.  이것은 누군가가 웹서버를 하나 만들어 두고, 거기에서 단 하나의 웹서버 소프트웨어를 구동한다.  대개 아파치를 사용한다.  그리고, 사용자들에게 사용할 수 있는 개인 저장공간을 제공한 다음, 이곳을 아파치의 가상호스트로 연결한다.  가장 값싸고, 효율적인 환경이었다.  일단 기계값과 인터넷 연결 비용만 내고 나면, 나머지는 모두가 오픈소스 소프트웨어를 무료로 사용하면 되는 것이다.  

그런데, 오픈소스 소프트웨어를 사용할 때에는 가장 골치아픈 문제가 바로 버전 관리이다.  버전이 올라갈 수록 새로운 기능이 추가된다.  또는 버그가 사라진다.  그러면, 특정 버전의 소프트웨어에 **의존하는** 다른 소프트웨어도 이에 대응하여 버전을 올리게 된다.  예를 들어, 위에서 블로그를 만드는 동적 소프트웨어의 대표적인 것이 워드프레스라고 했는데, 워드프레스는 **php** 라는 동적 웹페이지 생성용 스크립트 (프로그래밍 언어)로 짜여진 것이다.  그러니, 만약 php의 버전이 올라가면 (즉 업데이트가 되면) 조만간 워드프레스도 업데이트를 해야 한다.  웹호스팅 업체에서 php를 업데이트해주지 않았다면, 나는 워드프레스를 업데이트할 수 없다.  즉, 최신 기능을 사용할 수 없게 된다.  또는, 보안상 내지는 기타 버그를 안고 살아 가야 한다.

게다가 루비, 파이썬, 최근에는 자바스크립트와 Node.js의 등장으로 판도가 확 뒤바뀌게 되었다.  문제는 이렇게 나눠 쓰는 호스팅 서비스로는 이런 혜택을 누릴 수가 없게 된 것이다.  과거처럼 워드프레스와 같은 소프트웨어를 사용할 때와는 전혀 다른 수준의 자유를 누릴 수 있게 되었다.

과거에도 조금 더 비싼 호스팅 업체에서는 이런 프로그래밍 언어도 스스로 설치하여 사용할 수 있게 해 주었다.  다른 대안으로는 독립형 호스팅 내지는 서버 호스팅을 통하여 아예 기계 자체를 통째로 빌려서 쓰는 것이었다.  예상했겠지만, 단점이 아주 많다.  첫째, 돈이 아주 많이 든다.  둘째, 서버 전체를 직접 관리해야 한다.  그냥 적당히 타협하고 사는게 정답이다 (이었다).  적당히 업데이트 자주 해 주는 호스팅 사이트 골라서 사용하고, 호스팅 회사에서 자주 업데이트해 주는 은총만을 기다리는게 정답이었다.

## 그런데 왜 지킬을 사용하지?

이런 모든 상황이 확 바뀌게 된 것은 몇년 전부터 갑자기 유행하게 된 **구름 속의 컴퓨터** 즉 클라우드 컴퓨팅 덕분이었다.  이제는 구글, 아마존 등등에서 아주 싼 값에 마치 자기 서버를 운영하듯이 사용할 수 있게 된 것이다.  게다가, 무료로 또는 아주 싼 값에 저장공간만 빌려 쓸 수 있는 곳이 아주 많아졌다.  역설적이지만, 그러면서 정적 사이트 생성기의 가치를 다시 보게 되었다.

만일 남들과 다른 서비스나 다음으로 세상을 바꿀 뭔가를 만들고 싶다면 노드를 쓰면 될 일이다.  아니면, 그냥 많아야 하루에 한두번 업데이트하는 블로그를 쓸 바에는 동적인 사이트 생성기는 필요 없다.  정적 사이트 생성기이면서, 어디에나 잘 적응하는 지킬이 딱 좋다.  내가 **그 많은 블로그 소프트웨어를 써 보고 나서** 지킬로 정착한 이유이다.  내가 지킬을 가장 좋아하는 이유는:

1. 내가 원하는 편집기를 사용할 수 있다.  나는 [아톰](https://atom.io/)을 가장 좋아하지만, [submlime text](http://www.sublimetext.com/)를 쓰는 사람도 많고, 전설의 [vi](http://www.vim.org/)를 쓸 수도 있다.
2. 가장 싼 값에 홈페이지를 만들 수 있다.  공짜로 쓰려면 [github pages](https://pages.github.com/) 및 [gitlab pages](https://pages.gitlab.io/)를 써도 좋다.  약간 돈이 있다면 [아마존 s3](https://aws.amazon.com/s3/)같은 것을 써도 좋다.  과거처럼 호스팅 업체를 사용해도 좋고, 그렇지 않으면 간단히 파일만 저장하는 곳을 이용해도 무방하다.  상세한 점은 아래에 정리하겠다.  한 마디로 블로그를 만드는 가장 싼 방법이다. 
3. [git](https://git-scm.com/), [github](https://github.com/), [gitlab](https://about.gitlab.com/) 등의 버전관리 프로그램을 이용할 수 있다.
4. 데이터베이스를 이용하지 않으므로 백업이 간단하다.  데이터베이스 엑스포트를 하지 않고, 그냥 텍스트 파일을 다른 곳으로 복사하면 그만이다.  위에서 말한 깃을 사용해서 백업해도 좋다.
5. 데이터베이스를 이용하지 않으므로 간편하다.
6. [pandoc](http://pandoc.org/) 등을 이용하여 다른 여러가지 형태로 재가공이 용이하다.
7. [마크다운](https://daringfireball.net/projects/markdown/)과 [liquid](https://github.com/Shopify/liquid/wiki)가 아주 편리하다.  마음에 들지 않으면, 다른 것을 써도 좋다.

무엇보다도 이렇게 간단한 프로그램으로 이렇게 괜찮은 것을 많이 할 수 있다는 감탄 때문이다.

## 미리 알아 두고 해야 할 것들

불행히도, 공부를 좀 해야 한다.  오히려 이것 때문에 행운이라고 할 수도 있다.  일단, 불가능하지는 않지만 윈도우에서 제대로 다루기가 아주 까다롭다.  [윈도우 사용자가 주의해야 할 점 (설치 포함)](https://jekyllrb.com/docs/windows/) 페이지가 있지만, 그래도 까다로운 것은 사실이다.  가장 이상적인 환경은 맥이다.  따라서 맥에서 [iTerm2](https://www.iterm2.com/) 정도 프로그램은 열어 보고, [bash](https://www.gnu.org/software/bash/) 정도는 한두 번은 써 보았어야 한다.  

윈도우에서 잘 안된다고 했는데, 가장 큰 이유는 [Ruby](https://www.ruby-lang.org/en/)이다.  따라서, 루비 정도는 모두 섭렵할 필요는 없어도 약간 기초 정도는 알아 두는 것도 좋다.  몰라도 무방하다.

그리고, [마크다운](https://daringfireball.net/projects/markdown/)과 [liquid](https://github.com/Shopify/liquid/wiki)도 배우면 좋다.  나중에 정리할 계획이다.

## 터미널의 쌩기초

앞에서 WYSWYS, 즉 원하는 대로 문서를 포매팅하면 그 결과를 그 즉시 화면에서 볼 수 있는 새로운 기술이 나오기 전에 마크업이라는 언어가 있다고 말했다.  여기서 우리가 관심을 갖는 마크업 언어는 [HTML](https://en.wikipedia.org/wiki/HTML)이고, 이 언어는 1980년에 처음 나왔다.  그렇지만, 마크업 언어의 원조격이라 할 수 있는 언어인 [TeX](https://en.wikipedia.org/wiki/TeX)은 1978년에 나왔다.  WYSWYG가 나오면서 마크업 언어는 사라질 것 같았지만, (솔직히 비중이 줄어들긴 했지만) HTML은 여전히 건재하다!

마찬가지로 마우스를 처음으로 컴퓨터에 사용한 것은 1973년이었지만, 유명해지기 시작한 것은 1984년이라고 한다 ([위키피디어 마우스](https://en.wikipedia.org/wiki/Computer_mouse)).  마우스와 아이콘이 쓰이기 시작하기 전에는 사람들은 터미널을 사용하였다.  요즘처럼 컴퓨터를 켜면 윈도우나 맥 OSX같은 그래픽 OS가 뜨기 시작한 것도 1980년대 이후이다 ([위키피디어 GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)).  그 이전에는 마우스도 없이, 그래픽도 없이 깜박이는 커서에 타이핑을 해야 했다.  이런 것을 [CLI](https://en.wikipedia.org/wiki/Command-line_interface)라고 한다.  CLI 역시도 사라지지 않았다.

편집에서 파워 유저가 되려면 *TeX* 같은 언어를 배워야 하고, 컴퓨터 파워 유저가 되려면 CLI를 배워야 한다.  윈도우에서도 터미널이나 [ConEmu](https://conemu.github.io/)같은 터미널을 배워야 하고, 맥에서도 내장 터미널이나 [iTerm](https://www.iterm2.com/)같은 터미널을 배워야 한다.  사실상 그렇게 나쁘지 않다.  마우스가 없다고 생각하고, 그냥 타이핑하면 된다.  타이핑이야 어차피 워드나 엑셀을 써도 하는 것 아닌가?

여기에서 말하는 것을 해 보려면 여기에서 나오는 대로 그대로 따라서 타이핑하면 된다.  다만, 그 전에 몇 가지는 기본적으로 알아야 한다.  아래에서는 생존에 꼭 필요한 터미널 사용에 대해서 정리하였다.  더 자세한 내용은 [bash tutorial](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html) 등을 참고하라 ([bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell))는 맥이나 리눅스에서 에서 터미널을 사용하면 기본적으로 뜨는 셸 프로그램이다).  배우면 절대로 후회하지 않을 것이다.  

디렉토리에서 디렉토리로 이동할 때, 마우스가 아니라 *cd* 라는 명령어를 사용한다.  디렉토리를 나타낼 때에는 */* 을 쓴다.  현재 디렉토리는 마침표 하나 (*.*), 바로 위 디렉토리는 마침표 두 개(*..*)를 연달아 쓴다.  맨 위의 명령어를 생각해 보자.

~~~bash
$ jekyll new my-awesome-site
$ cd my-awesome-site
$ cd ..
~~~

첫번째 줄에서는 *jekyll* 이라는 프로그램을 실행시켰다.  이 프로그램은 사이트의 기본골격을 만들어 주었다.  그 전에, *my-awesome-site* 라는 디렉토리를 만들어서 그 속에 만들었다.  그 다음 줄의 *cd* 라는 명령어는 새로 만든 그 디렉토리로 이동하는 것이다.  그 다음 줄의 *cd ..* 명령어로 그 바로 위 디렉토리, 즉 원래 디렉토리로 되돌아왔다.

디렉토리의 내용을 볼 때에는 *ls* 명령어를 쓴다.  그리고, (맥에서만 통하는 방법이지만) 다음과 같이 입력하면 별도의 창에서 파인더가 뜬다.  *ls* 대신 디렉토리의 파일 내용을 볼 때 편하다.

~~~bash
$ open .
~~~

파일을 편집할 때에는 *vi* 또는 *nano* 같은 터미널상에서 돌아가는 편집기를 사용해도 되지만, [atom](https://atom.io/) 또는 [sublime text](https://www.sublimetext.com/)같은 프로그램을 써도 (쓰는 것이 더) 좋다.  터미널에서 다음과 같이 입력하라.  뒤에는 편집하고자 하는 파일 이름을 붙인다.

~~~bash
$ atom _config.yml
~~~

이전에 사용했던 명령어를 재사용하고자 하면 위쪽 화살표로 하나씩 볼 수 있다.  전체를 보고자 할 때에는 *history* 명령어를 사용한다.  파일명이나 디렉토리명을 다 쓰지 않고, 쓰다가 탭을 누르면 일치하는 파일이 하나밖에 없을 때에는 자동으로 파일명이나 디렉토리명을 채워 준다.  예를 들어 위의 명렁어의 경우 *atom _co* 까지만 친 상태에서 탭을 치면 나머지 파일 명을 자동으로 채워 준다.

## 텍스트 파일과 텍스트 편집기

사람에 따라 선호도가 다르다.  나는 개인적으로 [atom](https://atom.io/)을 선호한다.  프로그래머는 [sublime text](https://www.sublimetext.com/)를 더 좋아하는 것 같다.  나는 텍스트 파일을 많이 사용하지만, 아무래도 코드보다는 텍스트를 더 많이 다루기 때문인지 아톰이 더 편하다.

텍스트 파일에 대해서 가장 쉽게 이해하는 방법은 텍스트 파일이 아닌 것은 내용을 보거나 편집할 때 특별한 프로그램이 필요하다.  예를 들어, 워드 파일(docx)을 보고 편집하려면 마이크로소프트 워드가 필요하고, 이미지 파일을 보려면 이미지 뷰어가 필요하다.  그렇게 보고 작업을 하기 위해 어떤 특별한 프로그램도 필요하지 않으면, 대체로 텍스트 파일이라고 보면 된다.  참고로, 여기에서 말하는 *html* 이나 *markdown* 으로 작성한 파일은 거의 모두가 텍스트 파일이다.  *html* 파일의 경우, 웹 브라우저로 보면 필요한 처리를 모두 해서 깔끔하게 보이지만, 그렇다고 해서 *html* 파일을 보기 위해 반드시 웹 브라우저가 필요한 것은 아니다.  조금 지저분해 보이긴 하겠지만, 텍스트 편집기로 열어도 잘 보인다.  게다가 수정할 수도 있다.

많이 알면 많이 알 수록 더 좋겠지만, 자세한 내용을 몰라도 마이크로소프트 워드를 써 본 경험이 있다면, 텍스트 편집기에 적응하는 데에는 무리가 없다.

---

## 설치하기: 내가 사용하는 방법

맨 위에서 설치하기 방법을 설명했던 것으로 다시 돌아가 보자.

~~~bash
$ gem install jekyll bundler
~~~

이것은 컴퓨터에서 단 한 번만 실행한다.  이것은 기본적으로 지킬과 번들러라는 패키지를 설치하는 것이다.

~~~bash
$ jekyll new my-awesome-site
~~~

이 부분을 나는 다르게 한다.  이 명령을 실행하면, 지킬은 *my-awesome-site* 라는 디렉토리를 만들고, 그 디렉토리에 지킬이 실행하기 위해 (지킬이 실행한다는 것은 정적 웹페이지를 생성하고, 내장 웹서버를 실행시켜 웹서비스를 한다는 뜻이다) 필요한 파일을 만든다.  다른 방법은 지킬 스킨을 모아논 페이지에 가서 마음에 드는 것을 다운로드받아, 이것으로 기본적으로 생성되는 파일을 대체하는 것이다.  주로 사용하는 지킬용 스킨 페이지는 다음과 같다.

- [jekyll themes 1](http://jekyllthemes.org/)
- [jekyll themes 2](http://themes.jekyllrc.org/)
- [jekyll themes 3](http://jekyllthemes.io/)

여기에서 직접 다운로드를 받아도 되고, 아니면 여기에서 보통 [깃헙](http://github.com) 페이지로 연결되는데, 여기에서 *git* 명령어로 받아 와도 된다.  본 페이지를 만든 예인 [Ed](http://elotroalex.github.io/ed/)를 깃 명령어로 받아 오는 방법은 다음과 같다.

~~~ bash
$ git clone https://github.com/elotroalex/ed.git
$ cd ed
$ gem install bundler
$ bundle install
$ jekyll serve
~~~

### 노코기리 노트

[노코기리](http://www.nokogiri.org/)는 무엇이고, 왜 신경써야 하는가? 

> 노코기리, 또는 nokogiri 또는 "鋸" 은 HTML, XML, SAX, Reader의 파서이다. XPath 또는 CSS3 선택자를 통해 문서를 검색할 수 있는 특별한 능력이 있다. [노코기리 페이지](http://www.rubydoc.info/github/sparklemotion/nokogiri)에서

다 좋은데, 신경써야 하는 이유는 뭘까? 간단히 `gem install nokogiri`로 설치해서 그냥 사용하면 그만 아닌가? 위 페이지에서도 말하지만, [stack overflow](http://stackoverflow.com)에 가 보면 설치와 관련된 문제로 말 그대로 질문이 **오버플로** 하고 있다.  특히 맥에서... 루비를 사용하는 사람은 압도적으로 많은 수가 맥을 사용한다.  여하튼 해결방법은 몇 가지가 있다. 거의 비슷하다.  일단, 이렇게 해 보자.  특히 맥 OS의 버전이 업그레이드되고 나면, 이걸로도 해결될 수 있다.

~~~bash
$ xcode-select --install
~~~

이걸로 잘 안되면 다음 단계로 넘어가자.  이건 대부분 라이브러리 문제이다.  가장 쉽게 해결하는 방법은 다음과 같다.

~~~bash
$ export NOKOGIRI_USE_SYSTEM_LIBRARIES=Y
$ gem install nokogiri
~~~

혹시 그 전에 홈브루나 맥포트로 필요한 라이브러리를 설치해야 할 수도 있다.  다음 둘 중에 하나를 선택하라. 첫째는 맥포트로 필요한 라이브러리를 선택하는 것이다.

~~~bash
$ sudo port install pkgconfig libxml2 libxslt libiconv
~~~

두번째는 홈브루를 이용하는 것이다.

~~~bash
$ brew tap homebrew/dupes
$ brew install libxml2 libxslt
$ brew install libiconv
$ gem install nokogiri  -v '1.6.1' -- --with-iconv-dir=/usr/local/Cellar/libiconv/1.14/
~~~

세번째로 아무 것도 설치하기 싫다면, 다음 가운데 하나를 실행하라. 모두가 라이브러리 환경설정 관련된 설정을 바꾸는 방식이다.

~~~bash
$ sudo env ARCHFLAGS="-arch x86_64" gem install nokogiri -- --use-system-libraries  -- --with-xml2-include=/usr/local/Cellar/libxml2/2.9.2/include/libxml2 --with-xml2-lib=/usr/local/Cellar/libxml2/2.9.2/lib --with-xslt-lib=/usr/local/lib --with-xslt-include=/usr/local/include
$ gem install nokogiri -v '1.6.7.1' -- --use-system-libraries=true --with-xml2-include=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/usr/include/libxml2
$ ARCHFLAGS="-arch x86_64" gem install nokogiri -v '1.6.0'
~~~

추가 도움은 [노코기리 설치 페이지](http://www.nokogiri.org/tutorials/installing_nokogiri.html)를 참고하라.

## html, css, 자바스크립트: 홈페이지의 기본

*추가 예정*

## 지킬로 블로그 포스팅 쓰기

이제 기본적인 설치와 준비가 끝났으니, 글을 써 보자.  따지고 보면, 누군가가 이렇게 괜찮은 프로그램을 만든 것은 우리같은 평민이 글에 집중할 수 있도록 하기 위한 것 아니겠는가?  이걸 위해서는 몇 가지 배워야 하는게 있다.  첫째는 앞에서 말한 텍스트 편집기이다.  모든 포스팅은 텍스트 파일로 저장하여야 한다.  둘째로 배워야 하는 것은 **YAML** 그리고 이걸 이용한 **front matter** 이다.  마지막으로, 앞에서 누누히 이야기한 **markdown**이다.  여기에서는 뒤의 두 가지를 간단히 설명하겠다.

### front matter란 무엇인가?

정적 사이트 생성기는 데이터베이스를 쓰지 않는다.  동적 사이트 생성기는 데이터베이스를 쓴다.  데이터베이스란 한 마디로 엑셀 파일이라고 생각하면 된다.  각 줄을 하나의 글이라고 생각해 보자.  첫 칸에는 제목, 둘째 칸에는 날짜, 셋째 칸에는 저자명, 넷째 칸에는 주소, 다섯째 칸에는 태그, 그리고 여섯째 칸에는 내용을 쓴다.  예를 들자면...  정적 사이트 생성기는 어떻게 할까?  텍스트 파일을 만든다.  그러므로, 여기에 내용을 쓴다.  그럼 나며지는?  다행히도 본문은 양이 많겠지만, 나머지는 짧은 내용들로만 들어차게 될 것이다.  여기에서 본문을 제외한 나머지를 한군데 모아 넣을 수 있어야 한다.  이런 것들을 **front matter** 에 모아 둔다고 생각하면 된다.  예를 들자면, 다음과 같다 (내가 쓴 블로그 포스트의 예이다).

~~~ yaml
---
layout: post
title: "블로그 다시 시작하기"
slug: "start-over"
date: 2016-10-07 01:00:00 +0900
categories: blog
---
~~~

위에서처럼, 맨 첫 줄에 세 개의 대시(-)로 시작하고, 맨 마지막에도 세 개의 대시로 끝낸다.  그 사이에 본문이 아닌 모든 내용을 집어 넣는다.

첫 줄에서는 레이아웃을 정한다.  여기에서는 *default* 를 쓰도록 했다.  그 말은 여러 개의 레이아웃을 가질 수 있다는 말이다.  그리고, 블로그 포스트별로 다른 레이아웃을 지정할 수 있다는 말이다.  괜찮은데?  레이아웃은 모두 *_layouts* 디렉토리에 저장한다.  어떻게 다른 레이아웃을 만드는지는 아래에서 설명하겠다.

다음 줄에는 제목이 있다.  그리고, 그 다음 줄의 *slug* 은 한글 제목을 붙일 때에는 필요하다.  포스트의 주소에서 흔히 제목을 사용하는데, 제목이 한글일 경우 또는 영어인데 너무 긴 제목이거나 아니면 뭔가 밝히기 힘든 이유에서 제목과 주소를 다르게 하고 싶을 때 사용한다.  없어도 된다.

참고로, 이렇게 만든 포스트를 *_posts* 디렉토리에 만들어야 한다.  그리고, 파일 이름도 아무렇게나 지으면 안된다.  위의 예와 같은 경우에는 이렇게 지어야 한다.

~~~bash
2016-10-07-start-over.md
~~~

그러면, 파일명의 날짜와 frontmatter의 날짜가 싸우면 누가 이길까?  해 봤는데, frontmatter가 이긴다.

날짜는 두 번 쓴다.  파일 내에도 날짜를 쓰지만 (사실 안써도 무방하다), 쓸 때는 위의 포맷으로 쓴다.  즉, *연도-월-일* 그리고 *시-분-초* 그리고 시간대 (서울은 *UTC +0900* 이다.  기타 시간대는 [time zone](https://en.wikipedia.org/wiki/Time_zone) 참고)를 순서대로 쓴다.  

카테고리도 있어도 되고 없어도 되지만, 쓰려면 이렇게 쓴다.  기타 쓰고 싶은 것은 다 써도 된다.  기본적으로 설정된 내용은 [front matter](https://jekyllrb.com/docs/frontmatter/) 페이지를 참고하라.

위 문서에 따르면, 사전 정의된 *글로벌* 변수(즉 어디에서나 쓸 수 있는 것)에는 다음이 포함된다.

- layout: 사용할 레이아웃의 이름.  *_layouts* 디렉토리에 저장한다.
- permalink: 해당 페이지의 주소
- published: 참/거짓이다.  거짓으로 놓으면 아직 보이지 않는다.

또, 블로그 포스트에서만 쓸 수 있는 변수는 다음과 같다.

- date: 작성한 날짜.  오늘보다 뒤쪽이면 보이지 않는다.  그날에 다시 컴파일하면 보인다.
- category/categories: 카테고리.  복수형으로 쓰면 [YAML list](https://en.wikipedia.org/wiki/YAML#Basic_components)로 여러 개를 지정할 수 있다.
- tags: 위와 같다.

이 외에도 원하는 것은 어떤 것이라도 집어 넣을 수 있다.  예를 들자면, 나는 [영리하게 일하기](/smart-index.html) 폴더에 있는 내용은 날짜순으로든 날짜 역순으로든 정리되는 걸 원하지 않는다.  어차피 블로그가 아닌 것이다.  나름의 논리에 따라서 정렬되기를 원한다.  나는 YAML을 사용하여 이 문제를 정리하였다.  front matter에 우선 order라는 항목을 만들고 번호를 붙인다.  다음과 같이:

~~~yaml
order: 001
~~~

그 다음에는 포스트 페이지에 이렇게 yaml로 글의 순서를 order에 따라서 정렬하도록 한다.

~~~html
<ul class="post">
{% raw %}{% assign sorted = (site.smart | sort: 'order')  %}{% endraw %} 
{% raw %}{% for item in sorted %}{% endraw %}
<li class="post-title">
  <a href="{{ site.baseurl }}{{ item.url }}">
    {% raw %}{{ item.title }}{% endraw %}
</li>
{% raw %}{% endfor %}{% endraw %}
</ul>
~~~

그리고, 혹시 *YAML* 이 무엇의 약자인지 궁금한 사람이 있다면, 이 글을 죽 읽은 사람이라면 *ML* 은 *markup language* 의 약자임을 알 것이다.  나머지는 농담이다.  언젠가부터 유닉스 사용자들이 사용하던 철학적으로 말하자면 [자기참조적인](http://plato.stanford.edu/entries/self-reference/) 내지는 프로그래밍으로 말하자면 [재귀적인](https://en.wikipedia.org/wiki/Recursive_definition) 농담이다.  *YAML Ain't Markup Language* 그러니까 *YAML은 마크업 언어가 아니다* 의 약자이다.  비슷한 것으로는 *GNU* (GNU's Not Unix) 및 *PINE* (Pine Is Not Elm) 등이 있다.

### markdown의 생기초

문단을 나눌 때에는 엔터를 두 번 친다.

~~~markdown
첫번째 문단이다.

두번째 문단이다.
~~~

이렇게 되는 것이다.  기울여 쓰기(이탤릭)는 * 하나로, 두껍게 쓰기는 * 두개로 쓴다.

~~~markdown
*기울여* 쓰기와 **두껍게** 쓰기
~~~

링크는 다음과 같이 한다.

~~~markdown
[링크 텍스트](http://hyunkim.lawyer)
~~~

번호 없는 나열 (unordered list)과 번호 있는 나열 (ordered list)는 다음과 같다.

~~~markdown
* 번호 없는 나열 첫째
* 둘째

1. 번호 있는 나열 첫째
2. 둘째
~~~

이걸로 끝이다.  좀 더 자세한 내용은 아래에 정리하겠다.  다음으로 넘어가기 전에, 마크다운에서는 html의 모든 포매팅을 지원하지 않는다.  상응하는 마크다운 포맷을 찾을 수 없으면, 그냥 html을 쓰면 된다.  예를 들어, 마크다운에서는 밑줄을 지원하지 않는다.  그러면, 그냥 html에서처럼,

~~~markdown
<u>밑줄 치기</u>
~~~

와 같이 하면 된다는 뜻이다.

## 환경설정하기

모든 환경설정은 *_config.yml* 파일에서 한다.  *jekyll new* 명령을 사용했건, 아니면 스킨을 다운로드받아 사용했건, 이 파일을 처음부터 새로 만들 일은 없을 것이다.  [지킬의 환경설정 페이지](https://jekyllrb.com/docs/configuration/)를 참고하여 수정하라.

---

## 꾸미기

스킨은 위에서 링크한 사이트에서 다운로드받아 사용할 수 있다.  직접 만들 수도 있지만, 염두에 두고 있는 디자인에 가장 비슷한 것을 다운로드받은 것을 수정하는 것이 정신건강상 훨씬 좋다.  크게 세 가지를 수정하여야 한다.  직접 만들 때에도 세 가지를 손봐야 한다.

- *index.html* 또는 *index.md*
- *_layouts* 디렉토리
- *_includes* 디렉토리
- *assets* 디렉토리 (또는 기타 다른 디렉토리 아무데나)

### assets

이 디렉토리에는 보통 css, 자바스크립트, 이미지 파일 등을 포함시킨다.

### 조각 디렉토리

*_includes* 디렉토리에는 웹페이지의 조각들을 포함시킨다.  예를 들어, 모든 웹페이지에 공통되는 맨 위쪽과 맨아래쪽, 사이트바 등등 디자인에 공통되는 조각들을 포함시킨다.

### 레이아웃 디렉토리

보통 *_layouts* 디렉토리에는 적어도 하나의 파일이 포함된다.  *default.html* 이라고 하자.  이곳에 제대로 레이아웃 작업을 하되, *YAML* 을 이용하여, 위의 조각 디렉토리에 만들어 둔 것들을 포함시킬 수 있다.  예를 들면, 다음과 같다.

~~~yaml
<!DOCTYPE html>
<html lang="en-us">

{% raw %}{% include head.html %}{% endraw %}
~~~

이렇게 조각들을 적절한 위치에 집어 넣는 것이다.  만일 레이아웃을 많이 만들고 싶다면, 원하는 대로 만들어도 된다.  그럴 경우, 포스트 또는 페이지의 YAML front matter에 이렇게 지정하면 된다.  예를 들어 *poem.html* 이라는 레이아웃을 만들었다고 하면,

~~~yaml
---
layout: poem
title: O Captain! My Captain!
author: Walt Whitman
source: Poetry Foundation
---
~~~

같은 식으로 말이다.

### 지킬의 기본 변수

*추가 예정*

### liquid 이해하기

*추가 예정*

## 웹사이트를 올리기

### 깃헙 페이지

가장 쉬운 방법인데다가 가장 싼 방법은 바로 [깃헙 페이지](https://pages.github.com/)를 사용하는 것이다.  앞에서 지킬을 사용할 때의 강점 가운데 하나가 바로 [깃](https://git-scm.com/)을 사용하는 것이라고 말했다.  GIT은 리눅스를 만든 리누스 토발즈 (자기 이름을 따서 이름을 지은 것 맞다)가 만든 끝내 주는 버전 관리 프로그램이다.  [깃헙](https://github.com)은 깃을 이용한 프로젝트 관리를 용이하게 해 주는 사이트이다.  깃헙 페이지는 지킬을 이용하여 홈페이지를 - 무료로 - 만들 수 있도록 해 준다.  특히 IT 쪽으로 관심이 많다면, 이력서 겸 하나 만들어 두는 것도 좋다.

먼저 무료 아이디를 만들고, *repository* 를 하나 만든다.  아이디와 같은 이름으로 만들어야 한다.  그 다음에는 이걸 첵아웃해야 한다.  복잡하게 생각하지 말고, 서버에 있는 저장소 (repository)의 내용을 내 컴퓨터에 복사한다고 보면 된다.

~~~bash 
$ git clone https://github.com/username/username.github.io
~~~

일단 가지고 온 다음에는, 해당 디렉토리에서 원하는 대로 내용을 수정한다.  주의할 점은 여기에서 수정한 내용은 아직은 내 컴퓨터에만 있지, 서버에 있지 않다는 것이다.  그 다음에는 내 컴퓨터에서 작업한 파일을 서버에 올린다.  *push* 명령어를 이용한다.

~~~bash
$ git add --all
$ git commit -m "Initial commit"
$ git push -u origin master
~~~

조금 헷갈리겠지만, 이렇게 생각하면 된다.  깃은 기본적으로 버전 관리 프로그램이다.  그러므로, 버전에 대한 정보가 기록되어 있다.  그러므로, 내가 해당 디렉토리에서 작업한 모든 것은 아직은 버전관리 프로그램이 알지 못한다.  맨 처음의 *add* 명령은 내가 작업한 내용을 깃에 추가하는 것이다.  다음 명령어 *commit* 는 이걸 새로운 현재 버전으로 만드는 것이다.  *m* 다음에는 버전에 대한 정보를 입력한다.  그러므로, *add* 명령과 *commit* 명령으로 내가 작업한 내용을 저장소에 추가하였다.  그리고, 마지막 명령어인 *push* 를 통하여 내 컴퓨터의 저장소에 있는 내용을 서버의 저장소로 복사한다.  그러면 끝이다.

아마도 그 다음에는 [인터넷 주소 바꾸기](https://help.github.com/articles/setting-up-a-custom-domain-with-pages) 정도를 알고 싶을지도 모르겠다.

### 깃랩 페이지

**추가 예정**

### 아마존 S3

클라우드 컴퓨팅이 뭔지 모른다면, 아마존 웹 서비스는 최상의 교육 공간이다.  클라우드 컴퓨팅을 제공하는 업체는 아주 많지만, 사실상 아마존, 구글, 마이크로소프트에서 하나를 고르는게 어쩔 수 없는 현실이다.  컴퓨터를 구름 위에 올리면 아주 편할 것은 사실이다.  그렇지만, 절약하는 돈 만큼은 스스로의 노력으로 극복해야 한다.  요즘은 [도커](https://www.docker.com/)같은 서비스가 나와서 많이 좋아지긴 했지만, 여전히 클라우드 컴퓨팅의 학습곡선은 가파르고, 각 플랫폼별로 서로 다른 접근법을 취하고 있어 한 곳에서 배운 것이 그 대로 다른 곳으로 이전되지는 않는다.  개인의 관점에서는 하나를 선택해서 그냥 그걸 그대로 사용하는게 학습곡선을 줄이는 데에는 최선이다.  

[아마존 웹 서비스](https://aws.amazon.com/) 홈페이지를 가 보면 너무나도 많은 서비스가 존재한다.  그렇지만, 가장 기본적으로 알아야 하는 것은 EC2와 S3이다.  EC2의 맨 마지막의 숫자 "2"는 바로 앞의 글자 "C"가 두 개 있다는 뜻이다.  즉, ECC이고, 이것은 한 걸음 더 나가서 "Elastic Compute Cloud"이다.  우리가 흔히 클라우드 컴퓨팅이라고 부르는 것의 전형이다.  여기에서 "Elastic"하다는 것은 저장공간, 트래픽, CPU (특히 CPU) 등을 원하는 대로 유연하게 더하고 뺄 수 있다는 뜻이다.  지킬을 호스팅하기 위해 사용할 서비스는 이것이 아니다.

지킬의 강점 가운데 하나가 자원이 거의 들지 않으므로, 자신이 가지고 있는 최소한의 컴퓨팅 파워만으로도 사용할 수 있는 것이다.  솔직히 지킬 사용하려면 "EC2"까지는 필요 없다.  S3만 해도 충분하다.  여기서도 마찬가지로 숫자 "3"은 바로 앞의 글자가 3번 반복된다는 뜻이므로, SSS이고, 이것은 "Simple Storage Service"이다.  한 마디로 저장공간만 제공받는 것이다.  그런데 여기에 지킬을 사용할 수 있는 이유는 간단한 웹 서비스가 포함되기 때문이다.  앞의 EC2가 가상서버 호스팅이라면, S3는 그냥 공유 웹 호스팅이라고 보면 쉽다.  S3를 이해하려면, 당연히 S3를 이해해야 하지만, 여기에 더하여 Route 53도 배워야 한다.  이것은 다른 서비스에도 다 적용되는 내용이므로 한 번 배워 두는 것이 좋다.

#### Route 53

뒤에 "3"이 붙어 있다고 해서 5가 세 번 나오는 555는 아니다.  이것은 단지 포트 번호이다.  이 서비스가 하는 역할은 "라우팅" 즉 트래픽을 특정 방향으로 보내 주는 것이다.  예를 들어, S3에 지킬 서비스를 호스팅했다고 하면, 인터넷 주소, 예를 들어 [http://hyunkim.lawyer](http://hyunkim.lawyer)을 입력하면 해당 S3 버킷으로 보내 주는 것이다.

논리적으로, 라우팅을 설정하자면, 세 곳에서 설정을 해 주어야 한다.  첫째, 서비스를 제공하는 내용이 (여기 설명을 따라간다면, 지킬로 만든 서비스가) 인터넷 어딘가에 있어야 한다 (S3 버킷 설정).  둘째, 인터넷 주소 (예를 들면, [http://hyunkim.lawyer](http://hyunkim.lawyer))이 있어야 한다 (도메인).  그리고 마지막으로, 이 두 곳을 연결해야 한다.  이것이 두 단계이다.  첫째, 도메인을 서비스하는 곳에서 우선 인터넷 주소로 오는 모든 요청을 아마존으로 보내야 하고, 둘째는 아마존에서 그런 요청을 S3 버킷으로 보내야 한다.

우선, [S3 콘솔](https://console.aws.amazon.com/s3/)로 가서 로그인하고 (아니면 아이디를 만들라.  1년간 무료이다), 버킷을 2개 만든다.  하나는 도메인 이름 자체 (예를 들어, hyunkim.lawyer), 다른 하나는 여기에 "www"를 붙인 것 (예를 들어, www.hyunkim.lawyer)을 만든다.  둘 가운데 어떤 것을 실제로 사용할지 선택한다.  예를 들어, 인터넷의 표준은 *www* 를 붙이는 것이다.  그렇지만, 나는 개인적으로 이걸 붙이지 않는 것을 선호한다.  왜냐하면, 일단 타이핑하는 속도를 줄여주고, 둘째로는 웹 브라우저로 웹이 아니면 달리 뭘 쓰겠는가?  물론 웹 브라우저로 ftp나 다른 서비스를 사용할 수도 있지만, 그럴 때에는 주소에 다른 것을 앞에 추가하면 되지, 이미 표준이 되어버린 웹 서비스에 www를 추가하는 것이 괜한 낭비처럼 느껴지기 때문이다.  사람마다 선호는 다르다.  결론적으로 두 개의 버킷 가운데 하나는 실제로 사용하는 것이고, 나머지 하나는 다른 곳으로 보내 주는 역할을 한다.  그러니까, 나처럼 www를 뺀 서비스를 사용하고자 한다면, 만일 누군가가 www를 추가하여 요청을 보내면 이 요청을 www를 뺀 곳으로 보내야 하는 것이다.  그러므로, 우선 사용하지 않을 곳으로 가서 (예를 들어, www.hyunkim.lawyer), 다른 곳으로 보내는 설정을 한다.  이를 위해서는 *Redirect all requests to another host name* 을 선택하고, *Redirect all requests to* 다음의 빈칸에 실제로 사용할 주소 (예를 들면, hyunkim.lawyer)를 입력한다.  더 할 일은 많지만 (예를 들어 지킬로 만든 컨텐츠 올리기) 일단 집터는 만든 셈이다.  이제를 주소를 설정할 차례이다.

그 다음으로는 [Route 53 설정 페이지](https://console.aws.amazon.com/route53/home)로 가서, *Hosted Zone* 을 생성한다.  등록한 도메인 (예를 들어, hyunkim.lawyer)을 입력한다.  그러면, 두 개의 *Record Set* 이 만들어진다.  여기에서 *SOA* 는 지금은 그냥 무시해도 좋다 (만세!).  *NS* 에 가 보면 *Value* 에 네 개의 네임서버가 적혀 있다.  이걸 노트에 적거나, 노트패드같은 곳에 복사해 둔다.  

이걸로 끝이 아니다.  컴퓨터의 세상에서 문자는 다 가짜이다.  가짜 이름 말로 진짜 이름도 알아야 한다.  컴퓨터의 세상에서 진실은 다 숫자이다.  진실을 파악하는 무기는 윈도우에서는 *nslookup* 나머지 맥이나 리눅스나 유닉스에서는 *dig* 이다.  터미널에서, 아까 적어 둔 서버를 *dig* 해 보자.

~~~bash
$ dig ns-656.awsdns-18.net
~~~

이렇게 네임서버 4개의 진짜 이름을 파악한다.  그 다음으로 도메인을 등록한 (구매한) 곳에 가서 네밍서버로 이것들을 등록한다.  4개가 다 필요한 곳도 있고, 그보다 적게 필요한 곳도 있다.  

그 다음으로 꼭 해야 하는 것이 있는데, Record Set 두 개를 더 만들어야 한다. 나 같은 경우는 hyunkim.lawyer 과 hyunkim.lawyer 두 개를 만드는데, (이미 만들지 않았냐고? 앞에서 만든 것은 *NS* 와 *SOA* 이고 지금 만들 것은 *A Record* 이다. 이걸 하지 않으면 제대로 돌아가질 않는다.) 둘다 *Alias* 를 선택하고 (즉, 가명이라고 말해 주는 것이다), *Alias Target* 을 선택해야 한다. 버킷을 제대로 만들었다면, 자동으로 나타날 것이니 그 가운데 선택만 하면 된다.

#### S3 버킷에 지킬에서 작업한 내용을 올리기

앞의 내용을 따라했다면, S3 버킷이 두 개 있을 것이다.  하나는 가짜, 하나는 진짜.  진짜로 간다.  여기에서 *Static Website Hosting* (정적 웹사이트 호스팅: 앞에서 말한 것처럼 지킬은 정적 웹사이트 제조기이다) 다음에는 *Enable website hosting* (웹사이트 호스팅 사용하기)을 선택한다.

그리고, 잊지 말아야 하는 것이 바로 위의 *Permissions* 로 가서, *Edit bucket policy* 를 선택한 다음, *bucket policy* 를 입력한다.  *bucket policy* 는 이렇게 만든 S3 버킷을 어떻게 사용할지에 대한 것이다.  한 마디로 이걸 어떻게 서비스하고, 누가 쓸 수 있게 하는지 지정하는 것이다.  예를 들면, 다음과 같다.

~~~
{
	"Version": "2008-10-17",
	"Statement": [
		{
			"Sid": "PublicReadForGetBucketObjects",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:**",
			"Resource": [
				"arn:aws:s3:::example.com/*",
				"arn:aws:s3:::example.com"
			]
		}
	]
}
~~~

웹 서버의 설정은 당연히 누구나 읽을 수 있도록 하는 것이다.  좀 더 복잡하게 하고 싶다면, [Editing bucket permission](http://docs.aws.amazon.com/AmazonS3/latest/UG/EditingBucketPermissions.html) 및 [Bucket policy examples](http://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html)를 읽어 보라.

그 다음으로 할 일은 지킬에서 사용할 사용자 아이디와 비밀번호를 만드는 것이다.  뭐가 이렇게 복잡한지 생각이 들면 이렇게 생각해 보라.  블로그 사용자야 간단히 한 사람이겠지만, 클라우드 컴퓨팅의 접근법은 그렇지 않다.  이것은 구름 위에 컴퓨터를 올려 놓고 여러 사람이 함께 사용하는 것이다.  따라서, 이미 사용하는 아마존 아이디는 관리자 아이디이고, 지금 만드는 아이디는 실제 클라우드를 사용할 (여기의 예에서는 웹서버를 만들고 글을 올리고 관리할) 사용자이다.  [AWS IAM Console](https://console.aws.amazon.com/iam/)로 가서, 새로 사용자를 만든다. 사용자 아이디와 (자동으로 생성되는) *access Key ID* 그리고 *Secret Access Key* 값을 받아 적는다.

지킬은 루비로 만든 사이트이다.  복습하자면, 루비에서 패키지는 보석쪼가리 *gem* 으로 한다.  여기에서 우리는 *s3_website* 라는 보석쪼가리 즉 소프트웨어를 사용할 것이다.  이 소프트웨어가 하는 일은 지킬로 만든 사이트를 S3에 올려 주는 일이다.  보석쪼가리를 설치하자.

~~~bash
$ gem install s3_website
$ s3_website cfg create
~~~

첫번째 명령어는 보석쪼가리를 설치하는 것이고, 두번째 명령어는 이 보석쪼가리를 사용하는 것이다.  두번째 명령어를 실행하면, *s3_website.yml* 이라는 환경설정 파일을 만들어 준다.  맨 앞의 세 줄만 수정하면 된다.

~~~
s3_id: access Key ID
s3_secret: Secret Access Key
s3_bucket: example.com
~~~

앞에서 정신 없이 적어 놓은 것들이 이제야 결실을 보는 것이다!  아이디와 시크릿코드, 그리고 버킷 이름을 입력한다.  

앞에서 지킬로 만든 사이트를 보려면, *jekyll serve* 라는 명령어를 입력하고 (내 컴퓨터) 홈페이지에 가서 볼 수 있다고 했다.  이 명령어가 하는 일은 두 가지이다.

1. *_site* 디렉토리에 작업한 내용을 근거로 해서 정적 웹 사이트를 만든다
2. 내장 웹서버 프로그램을 가동하여 위 *_site* 디렉토리의 내용을 보여 준다.

또 하나 알아야 할 명령어는 *jekyll build* 이다.  이 명령어는 위의 두 번째 과정은 생략하고, 그냥 작업한 내용을 근거로 정적 웹 사이트를 만드는 첫번째 일만 한다.  이렇게 하면 (당연히) *_site* 디렉토리에는 여러분이 어렵게 만든 작품이 기다리고 있을 것이다.  이제 이 내용을 아마존 S3에 올리면 된다.

~~~bash
$ s3_website push
~~~

블로그 답게 새로 작업을 할 때마다 이 명령을 반복해 주면 된다.

### 일반 웹서버

일단 알아 두어야 하는 것은 지킬에서 *build* 명령어를 다음과 같이 수행하면,

~~~ bash
$ jekyll build
~~~

디렉토리 내의 *_site* 디렉토리에 html, css, 자바스크립트 파일을 포함한 모든 내용이 생성된다는 것이다.  그러므로, 서버의 환경에 따라 이 디렉토리의 내용을 통째로 복사해서 서버에 옮겨버리면 완성이다.  흔히 *ftp* 나 *rsync* 같은 것을 쓰지만, 환경에 맞추어 다양한 방법을 구사할 수 있다.  기본적인 아이디어는 [jekyll deployment](https://jekyllrb.com/docs/deployment-methods/) 페이지에서 확인할 수 있다.

**추가 예정**

---

## 페이지: 컬렉션

블로그의 포스트가 아닌 페이지는 어떻게 만드는가?  한 가지 방법은 [페이지를 만드는](https://jekyllrb.com/docs/pages/) 것이다.  매뉴얼에서는 두 가지 방법을 소개하고 있지만, 하나만 쓰면 된다.  첫째는, 기본 디렉토리에 확장자가 *html* (html 파일인 경우) 또는 *md* (마크다운 파일인 경우)인 파일을 만드는 것이다.  이럴 경우 주소는 그 파일명 (다만 확장자는 html)이다.  예를 들어, 홈페이지에 *about.md* 라는 파일을 만들었다면, 주소는 *about.html* 이 되는 것이다.  두번째는 기본 디렉토리에 디렉토리를 하나 만들고, 그 안에 *index.html* 또는 *index.md* 파일을 넣는 것이다.  이 경우 주소는 파일이 속한 디렉토리명이다.  예를 들어, */about/index.md* 파일을 만들었다면, 주소는 */about/* 이다.  사실 이것만 가지고도 아주 많은 것을 할 수 있다.  예를 들어, front matter에 *permalink* 를 이용하여 온갖 종류의 디렉토리 구조를 다 만들 수 있다.  다만, 이럴 경우, 기본 디렉토리의 내용이 너무 복잡해진다.  즉, 관리가 안된다.  이럴 때 쓸 수 있는 것이 컬렉션이다.

컬렉션은 페이지와 비슷하지만, 몇 가지 특성을 공유하는 (예를 들어, 똑같은 레이아웃을 쓰는) 파일들의 집합이다.  가장 쉽게는 디렉토리만 공유하는 컬렉션을 만들 수도 있다.  컬렉션을 만들려면, 우선 *_config.yml* 에 다음과 같이 입력한다.

~~~yaml
collections:
  my_collection:
    output: true
    permalink: /awesome/:path/
~~~

맨 위의 두줄은 컬렉션을 지정하는 것이다.  이렇게 지정한 컬렉션의 이름은 *my_collection* 이 된다.  그 아래에는 컬렉션과 관련된 환경설정이다.  첫줄은 문서를 볼 수 있게 해 준다 (볼 수 없게 하려면 왜 컬렉션을 만들어?  믿거나 말거나, 그런 경우도 있다).  둘째 줄은 인터넷 주소를 이렇게 쓰라고 알려 준다.

그 다음에는 디렉토리를 만들고, 파일을 만들어 넣는다.  주의할 점은 컬렉션 명이 *my_collection* 이라면, 디렉토리명은 *_my_collection* 이 되어야 한다는 것이다 (즉, 밑줄부호를 맨 앞에 붙일 것).

이걸 *liquid* 에서 구현하고 할 때에는 *site* 를 이용한다.  예를 들어, 모든 블로그 포스트는 *_posts* 디렉토리에 들어가야 하고, *site.posts* 변수로 접근 가능하다.  모든 페이지는 기본 디렉토리에 있어야 하고, *site.pages* 로 접근할 수 있다.  위에서처럼, *my_collection* 이라는 컬렉션을 만들었다면, 그 내용은 모두 *_my_collection* 디렉토리에 들어가야 하고, *liquid* 작업을 할 때에는 *site.my_collection* 으로 작업할 수 있다.  사용 예는 [매뉴얼 컬렉션](https://jekyllrb.com/docs/collections/)에서 찾아볼 수 있다.  이 페이지에서 드는 예는 *album* 이라는 컬렉션의 내용을 *liquid* 로 받아서 보여 주는 것이다.

~~~yaml
{% raw %}{% for album in site.albums %}{% endraw %}
  <h2>{% raw %}{{ album.title }}{% endraw %}</h2>
  <p>Performed by {% raw %}{{ album.artist }}{% if album.director %}{% endraw %}, directed by {% raw %}{{ album.director }}{% endif %}{% endraw %}</p>
  {% raw %}{% for work in album.works %}{% endraw %}
    <h3>{% raw %}{{ work.title }}{% endraw %}</h3>
    <p>Composed by {% raw %}{{ work.composer }}{% endraw %}</p>
    <ul>
    {% raw %}{% for track in work.tracks %}{% endraw %}
      <li>{% raw %}{{ track.title }} ({{ track.duration }}{% endraw %})</li>
    {% raw %}{% endfor %}{% endraw %}
    </ul>
  {% raw %}{% endfor %}{% endraw %}
{% raw %}{% endfor %}{% endraw %}
~~~

짐작했겠지만, 위 코드는 *album* 이라는 컬렉션에서 제목, 예술가, 감독, 작품별로 제목, 작곡가 및 트랙별로 제목, 길이 등의 정보를 받아 와서 그걸 목록으로 만들어서 보여 주는 예이다.  물론, *album* 이라는 컬렉션을 만들어, 위와 같은 식으로 정리해 두었어야 한다. 

## 데이터

간단히 데이터베이스 대신 쓸 수 있는 것이다.  데이터를 우선 *yml* 또는 *csv* 또는 *json* 포맷으로 만든다.  *_data* 라는 디렉토리를 데이터 파일을 만들어 거기로 옮긴다.

[지킬 매뉴얼](https://jekyllrb.com/docs/datafiles/)에서 드는 예는 다음과 같다.  *_data/members.yml* 이라는 파일에 다음과 같이 입력했다고 해 보자.

~~~yaml
- name: Eric Mill
  github: konklone

- name: Parker Moore
  github: parkr

- name: Liu Fengyun
  github: liufengyun
~~~

이걸 liquid를 이용하여 본문에 다음과 같이 정열하여 보여줄 수 있다.

~~~yaml
<ul>
{% raw %}{% for member in site.data.members %}{% endraw %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {% raw %}{{ member.name }}{% endraw %}
    </a>
  </li>
{% raw %}{% endfor %}{% endraw %}
</ul>
~~~

## 카테고리와 태그

*추가 예정*
## 유용한 팁

포스트에 대하여 링크를 하려면 다음과 같이 한다.

~~~markdown
{% raw %}[링크 이름]({% post_url 2017-01-01-post %}){% endraw %}
~~~
---

## 각주
