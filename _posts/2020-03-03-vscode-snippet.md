---
layout: post
title: "VS Code에서 Snippet 활용하기"
categories: ["how, vscode"] # suggestion: gtd, how, lawyering, news, stuff, books
excerpt: "VS Code에서 Snippet을 활용하여 항상 하는 일을 빨리 하기"
sharing:
  facebook: "VS Code에서 Snippet을 활용하여 항상 하는 일을 빨리 하기"
color-scheme: cyan # available: red, orange, green, cyan, blue, magenta, brown 
date: 2020-03-03 15:58:59 +0900
tags: 
math: # true possibly
# To include book: {% include book.html id='calstory' %}
# To include image: {% include image.html url='FN' description='description' alt='alt' %}
---

"남들보다 더 잘하거나, 아니면 남들보다 더 빨리하거나" -- 우리의 모토입니다.

원래 MS를 그리 좋아하지 않았지만, 요즘 들어서는 조금씩 더 좋아집니다. 가장 큰 두 가지 이유를 들자면, 하나는 [깃헙](https://github.com)을 인수한 것이고, 다른 하나는 [VS Code](https://code.visualstudio.com/)입니다. 특히 이것은 리눅스에서도 사용할 수 있도록 배려하였다는 것도 큽니다.

빨리 하기 위해 무엇보다도 항상 하는 일을 더 빨리, 손쉽게 하는 것이 필요합니다. 특히, 항상 쓰는 문장이나 문단 (계약서를 쓰건, 코딩을 하건) 은 스니핏(snippet)에 넣어 두면 아주 유용하죠. 예를 들어, 리눅스에서는 블로그에 글을 쓰려면 항상 특정 디렉토리로 갑니다. 그 다음에는 편집기 (VS Code)로 새 글을 씁니다. 이 과정을 간단히 하기 위해서는 홈 디렉토리의 `.bashrc`에 다음과 같이 넣어 둡니다. 내가 쓰는 블로그 내용을 홈 디렉토리의 `~/hyunkimlawyer`에 모아 둔다고 하면,

{% highlight bash linenos %}
function blog() { cd ~/hyunkimlawyer; }
function writeb() { code ~/hyunkimlawyer/_posts/`date +%F`-"$1".md; }
{% endhighlight %}

첫번째 줄은 블로그 사이트로 이동합니다. 두번째 줄은 새 포스트를 엽니다. 지킬에서 포스트는 모두 `_posts` 디렉토리에 있으며, 모두가 `날짜 + 제목 + .md` 형태를 띱니다. 예를 들어, 이 글의 경우에는 `2020-03-03-vscode-snippet.md` 형태입니다. 따라서 두 번째 줄은 앞의 디렉토리와 날짜를 모두 무시하고 제목만 하이픈으로 연결하여 입력한다면 바로 그 파일을 만들어 주는 것이죠. 이렇게요.

{% highlight bash linenos %}
$ writeb vscode-snippet
{% endhighlight %}

그 다음으로, 지킬에서는 [front matter](https://jekyllrb.com/docs/front-matter/)라는 것이 있어서, 여기에 내용과 별개로 필요한 것들을 -- 예를 들어, 제목, 날짜, 카테고리 등등 -- 기록하는데, 이것을 간단히 하려면, VS Code의 [Snippet](https://code.visualstudio.com/docs/editor/userdefinedsnippets) 기능을 이용하면 되는거죠.  예를 들어, 제 페이지의 경우, 다음과 같은 front matter가 있습니다.

{% highlight yaml linenos %}
---
layout: post
title: "VS Code에서 Snippet 활용하기"
categories: ["how, vscode"] # suggestion: gtd, how, lawyering, news, stuff, books
excerpt: "VS Code에서 Snippet을 활용하여 항상 하는 일을 빨리 하기"
sharing:
  facebook: "VS Code에서 Snippet을 활용하여 항상 하는 일을 빨리 하기"
date: 2020-03-03 15:58:59 +0900
tags: 
---
{% endhighlight %}

이걸 한 번의 키보드로 넣기 위해 다음과 같이 합니다. 메뉴에서 `File-Preferences-User Snippets`를 킄릭하고, 위에 나오는 검색창에서 확장자를 선택합니다. 저의 경우 `markdown`을 선택합니다. 그러면, `markdown.json` 파일이 열립니다. 거기에 내용을 입력합니다.

{% highlight json linenos %}
"Header": {
	"prefix": ["header", "hdr", "front-matter", "frontmatter"],
	"body": [ "---",
		"layout: post",
		"title: \"${1:제목}\"",
		"categories: [\"$2\"] # suggestion: gtd, how, lawyering, news, stuff, books",
		"excerpt: \"$3\"",
		"sharing:", 
		"  facebook: \"$4\"",
		"date: ${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE} ${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND} +0900",
		"tags: $5",
		"---",
		"",
	    "$0"],
	"description": "Creates YAML frontmatter",
},
{% endhighlight %}

먼저 첫줄의 `Header`는 제가 임의로 정한 이름입니다. 두번째 줄의 `prefix`에는 스니핏을 이용할 때 사용할 단어입니다. 대시(-)로 이은 단어는 그 앞머리만 입력해도 됩니다. 그러니까 위에서 `front-matter`를 정의해 놓았으므로, 이걸 그대로 써도 되고 `fm`이라고 써도 된다는거죠. `body`에는 입력할 내용, 그리고 `description`에는 여기에 대한 설명이 있습니다. 10번째 줄의 `date`에 있는 내용은 작성하는 때의 날짜와 시간을 받아서 자동으로 입력합니다. 이 글의 경우에는 다음과 같이 입력되었습니다. 사용할 수 있는 변수명은 [Snippets in Visual Studio Code](https://code.visualstudio.com/docs/editor/userdefinedsnippets)에서 `Variables` 페이지를 보시면 됩니다.

{% highlight yaml linenos %}
date: 2020-03-03 15:58:59 +0900
{% endhighlight %}

그리고, 5, 6, 7, 9, 10번째줄의 변수는 `Tabstops`라고 하는 것입니다. 맨 처음에는 텍스트를 입력한 다음에 `$1`이 있는 곳에 커서가 놓입니다. 그 다음에는 탭을 치면 순서대로 `$2`, `$3` ... 등으로 진행합니다. 그리고, 여기에 자동으로 입력할 내용을 `Placeholders`로 지정할 수 있습니다. 콜론 `:`으로 지정합니다. 예를 들어, 위에서는 `"title: \"${1:제목}\""` 자리에 `제목`이라는 글자가 자동으로 들어가 있는거죠. 그리고, `|` 속에 쉼표 `,`로 구분한 문자는 선택지입니다. 예를 들어,

{% highlight yaml linenos %}
[\"${2|gtd, how, lawyering, news, stuff,books|}\"]
{% endhighlight %}

이 위치로 가면 화살표로 카테고리를 선택할 수 있게 되는거죠. 그리고, 탭을 계속 따라가다가 맨 마지막에는 `$0`이 있는 위치로 가서 끝납니다.  항상 뭔가 써야 하는 사람이라면, 아주 유용하죠. 